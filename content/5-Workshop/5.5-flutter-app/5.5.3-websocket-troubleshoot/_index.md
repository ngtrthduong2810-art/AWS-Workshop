---
title: "End-to-End Testing and WebSocket Troubleshooting"
date: 2026-07-09
weight: 3
chapter: false
pre: " <b> 5.5.3. </b> "
---

#### 1. Incident: the new WebSocket route wasn't recognized by API Gateway

**Symptom:** after adding the `whoami` route (Lambda + Route + Integration) to `template.yaml` and getting a successful `sam deploy`, the Flutter app sent a `{"action": "whoami"}` request but always got back:

```json
{"message": "Forbidden", "connectionId": "...", "requestId": "..."}
```

Checking the CloudWatch Logs for the `inboxiq-ws-whoami` Lambda showed the log group **had never been created** — solid proof the request never reached the Lambda; the failure was at API Gateway's routing layer, not in the code.

![Log group does not exist](/images/5-Workshop/5.5-flutter-app/whoami-log-group-not-exist.jpg)

**Root cause:** checking the Console, the `WsWhoamiFunction`/`WhoamiRoute`/`WhoamiIntegration` resources all showed `CREATE_COMPLETE` in the CloudFormation stack — the route really had been created. But under **API Gateway → WebSocket API → Stages → prod → Deployment history**, the stage was still active on a deployment **older than the route's creation date** — meaning CloudFormation successfully created the `AWS::ApiGatewayV2::Route` resource, but **did not automatically create a new deployment for the `prod` stage**, even with `DependsOn` declared between `AWS::ApiGatewayV2::Deployment` and that route. `DependsOn` only guarantees creation order; it doesn't force CloudFormation to treat this as a "change" requiring a re-deploy.

![Deployment history showing only one stale deployment](/images/5-Workshop/5.5-flutter-app/deployment-history-stale.jpg)

**Fix:** go to the API Gateway Console → select the WebSocket API → **Deploy API** → choose the `prod` stage → confirm. Once a new deployment exists, the route works immediately, with no code changes or CloudFormation re-deploy needed.

![New deployment after manually deploying the API](/images/5-Workshop/5.5-flutter-app/deployment-history-fixed.jpg)

**Lesson:** with `AWS::ApiGatewayV2` managed through SAM/CloudFormation, adding a new route doesn't automatically mean that route is "live" on the running stage. Verify through the Deployment history after every route change, or consider designing the template so the `Deployment` logical ID changes with the route content (e.g. appending a hash) to force CloudFormation to create a new deployment every time.

#### 2. Incident: WebSocket "appeared connected" while the handshake was still in progress

**Symptom:** right after fixing the `whoami` route, the app still reported "WebSocket not ready" on some runs, inconsistently.

**Root cause:** the original code used:
```dart
_channel = WebSocketChannel.connect(uri);
await Future.delayed(const Duration(milliseconds: 300));
```
`WebSocketChannel.connect()` returns immediately, without waiting for the handshake to actually complete (which includes the time the Lambda Authorizer takes to verify the JWT — potentially longer than 300ms on a cold start). Sending a message before the handshake finished caused the message to be silently dropped, with no error thrown.

**Fix:** replace the fixed delay with the library's real readiness signal:
```dart
_channel = WebSocketChannel.connect(uri);
try {
  await _channel!.ready;
} catch (e) {
  _channel = null;
  rethrow;
}
```
`channel.ready` is a `Future` that only completes once the handshake succeeds, or throws if it fails — completely eliminating the need to guess a wait time.

#### 3. Incident: sequential email processing broke down at scale

**Symptom:** response time grew linearly with the number of emails; a single failed email (OpenAI timeout, rate limit) wiped out the results of every other email in the same batch.

**Root cause:** the original code called GPT-4o-mini sequentially inside a `for` loop, with each call having a 15-second maximum timeout — with many unread emails, the total time easily approached the Lambda Worker's timeout (300 seconds) and increased the risk of the client-side WebSocket connection closing before results could be received.

**Fix:** switched to parallel processing with per-item fault tolerance:
```js
const summaries = (await Promise.allSettled(
  emails.map(async (email) => {
    const summary = await summarizeWithOpenAI(email, apiKey);
    await saveSummary(userId, email.id, summary);
    return { emailId: email.id, ...summary };
  })
)).filter(r => r.status === 'fulfilled').map(r => r.value);
```
`Promise.allSettled` (instead of `Promise.all`) ensures one rejected item doesn't bring down the entire batch — a failed email is simply skipped, while the rest still return their results normally. The `maxResults = 10` cap on each `fetchUnreadEmails` call was kept in place to avoid blowing the Lambda timeout or causing an OpenAI cost spike if a mailbox has dozens of unread emails.

#### 4. Incident: `connectionId` hard-cached at the UI layer, causing silent `410 Gone` failures

This was the hardest-to-spot incident in the entire Flutter section, because no error message was ever shown to the user — the Check Gmail button just spun forever.

**Symptom:** the Worker Lambda's logs showed processing completed successfully (emails fetched, OpenAI calls succeeded, tokens billed on the OpenAI dashboard), but the final push step failed:

```
WARN WebSocket push failed for gTg3TG75DQAYKABzSA==: GoneException UnknownError
{"httpStatusCode":410, "requestId":"...", "attempts":1, "totalRetryDelay":0}
```

![GoneException 410 log when pushing over WebSocket](/images/5-Workshop/5.5-flutter-app/worker-gone-exception.jpg)

**Root cause:** cross-referencing timestamps between two logs:

| Time | Event |
|---|---|
| T | `ws-disconnect` Lambda records the connection as closed |
| T + 18s | User taps "Check Gmail" |
| T + 27s | Worker Lambda attempts to push to that connectionId → `410 Gone` |

The connection had already died **before** the user tapped the button, yet the app kept sending the old `connectionId`. The root cause was at the UI layer: the Home screen stored `connectionId` in `State` only once, inside `initState()`. When the WebSocket dropped (network change, app briefly leaving the foreground, or API Gateway closing an idle connection), the underlying service cleared its internal `connectionId` value to `null`, but the screen's `State` variable was **never synced to match** — leading to a stale value being used to call the API.

**Fix:** read `connectionId` directly from the service (the live source of truth) at the exact moment the button is tapped, and automatically reconnect if the value turns out to be `null`, instead of trusting the value cached in `State`:

```dart
Future<void> _checkGmail() async {
  var connId = _ws.connectionId;
  if (connId == null) {
    setState(() => _connectingWs = true);
    try {
      await _ws.connect();
      connId = await _ws.requestConnectionId();
      if (mounted) setState(() => _connectionId = connId);
    } finally {
      if (mounted) setState(() => _connectingWs = false);
    }
  }
  if (connId == null) {
    ScaffoldMessenger.of(context).showSnackBar(
      const SnackBar(content: Text('WebSocket chưa sẵn sàng')));
    return;
  }
  // continue calling checkGmail with connId
}
```

**Lesson:** for any long-lived connection (WebSocket, gRPC stream...), state displayed in the UI must always be re-verified at the source right before use, never trusted from a cache — because the connection can die at any moment with no event ever notifying the layer that called it.

#### 5. Other issues encountered and how they were resolved

| Issue | Root cause | Fix |
|---|---|---|
| `sam deploy` reports "No changes to deploy" despite `template.yaml` being edited | Ran `sam deploy` without rebuilding first — SAM packaged the stale build, whose hash matched what was already deployed | Always run `sam build` before `sam deploy` after editing the template or code |
| The Lambda Console table appeared to be missing a newly created function | The list view was limited/needed a refresh, not an actual missing function | Cross-verify through CloudFormation → Resources instead of trusting a single glance at the Lambda Console |
| App reports "WebSocket not ready" even though it had connected earlier | The old connection session had been closed (see item 4) | Read a fresh `connectionId` from the service, auto-reconnect when needed (see item 4) |

#### 6. Outcome

After this section, the entire InboxIQ pipeline runs completely on a real device, from tapping the button in the app to seeing the summarized results appear in real time over WebSocket, with no polling required:

```
Flutter App → Cognito Auth → REST API → SQS → Worker
  → Gmail API + GPT-4o-mini (parallel, per-item fault tolerant)
  → DynamoDB
  → WebSocket push → Flutter App renders SummaryCard
```

![List of summarized emails displayed in the app](/images/5-Workshop/5.5-flutter-app/summaries-displayed.jpg)

#### 7. Remaining items, noted as future maintenance work

- Add a `WidgetsBindingObserver` to automatically reconnect the WebSocket when the app returns from the background — currently the recovery mechanism only triggers when the user actively taps the Check Gmail button again
- Rotate the Google OAuth Client Secret (it was exposed once in a screenshot while requesting support during development)
- Build a Sign Up screen so new users can register their own Cognito account, instead of one being created manually via the Console — needed if the app expands to real, multiple users
- Upgrade the Lambda runtime off Node.js 20.x to a version with longer-term support, ahead of the real-world impact milestones (02/2027, 03/2027)
