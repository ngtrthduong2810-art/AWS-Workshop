---
title: "Flutter App & End-to-End Flow"
date: 2026-07-09
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

#### Why Flutter App needs its own section

The previous sections (Backend, Gmail OAuth) built out the entire server side, but end users don't call the API directly — they need a mobile app to sign in, connect Gmail, and view the summarized results. This section covers the Flutter client and, more importantly, the **real-time WebSocket push flow** — the hardest part of the whole project, because it doesn't show up on the architecture diagram at a glance, yet it's where most of the hard-to-spot bugs came from.

The complete flow from button tap to seeing a result:

```
User taps "Check Gmail" in the app
  → App sends connectionId (obtained via the whoami route) to REST /check-gmail
  → Lambda producer pushes a job onto SQS
  → Lambda Worker picks up the job from SQS
  → Worker calls the Gmail API for unread emails, calls GPT-4o-mini to summarize (in parallel)
  → Worker stores the results in DynamoDB
  → Worker pushes the results back to the app via API Gateway WebSocket (PostToConnection)
  → App receives the message over WebSocket and renders the list of SummaryCards
```

The key design decision: results are **not** fetched via periodic REST polling — there is no `GET /summaries` endpoint at all. Every result is pushed one-way from server to client over WebSocket the moment it's ready, cutting down API calls and delivering a genuine "real-time" feel. The price paid is complexity: the client has to manage the WebSocket connection's lifecycle itself, and has to know when a connection has gone "dead" so it can reconnect — this is what consumed most of the debugging time in this section.

#### Client architecture (instance-based)

Every service in the app (`AuthService`, `RestApiService`, `WebSocketService`, `GmailOAuthService`) is designed to be **instance-based** — created once at the app's root and passed down through constructors, rather than using static classes or global singletons. This approach makes testing and lifecycle management (disposing when a screen closes) much clearer, at the cost of a bit more constructor-parameter boilerplate.

Main folder structure:

```
lib/
├── config/app_config.dart          # Endpoint URLs, Cognito IDs
├── services/
│   ├── auth_service.dart           # Cognito login/signup
│   ├── rest_api_service.dart       # HTTP calls
│   ├── websocket_service.dart      # WebSocket connect + listen
│   └── gmail_oauth_service.dart    # OAuth init + deep link handler
├── models/email_summary.dart
├── screens/{login,home}_screen.dart
└── widgets/summary_card.dart
```

#### Issues encountered and how they were resolved

**1. `$connect` cannot safely return a `connectionId` immediately.** Sending a message right inside the `$connect` Lambda risks a `GoneException`, because the connection isn't necessarily fully "alive" yet at that point. Solution: add a dedicated WebSocket route called `whoami` — the client proactively sends a request after connecting, and the `ws-whoami` Lambda uses `ApiGatewayManagementApiClient` to safely return the `connectionId`.

**2. API Gateway doesn't automatically re-deploy the stage when a new route is added via CloudFormation.** The `whoami` route was successfully created in CloudFormation (`AWS::ApiGatewayV2::Route`), but the `prod` stage still pointed at the deployment that predated that route — even with `DependsOn` declared between the `Deployment` and the `Route`. The result: every `whoami` request was rejected by API Gateway with `Forbidden` right at the routing layer, never even reaching the Lambda. How it was detected: checking the target Lambda's CloudWatch Logs — a log group that has never been created is definitive proof the request never got there. The fix: proactively **Deploy API** to the correct stage after every route addition or change, rather than trusting `sam deploy` alone.

**3. `WebSocketChannel.connect()` in Flutter doesn't wait for the handshake to finish.** The function returns immediately even though the actual connection (including the Lambda Authorizer verifying the JWT) is still being processed behind the scenes. Using a fixed-duration `Future.delayed` is an unreliable guess — replaced with `await channel.ready`, a Future that only completes once the handshake succeeds, or throws if it fails.

**4. Processing emails sequentially made response time grow linearly and risked losing an entire batch over one failed email.** Originally, the Worker called GPT-4o-mini one email at a time inside a `for` loop. With 10 unread emails, each OpenAI call could take up to 15 seconds (the max timeout) — run sequentially, the total time easily approached the danger zone and increased the risk of the WebSocket connection closing before results could be returned. Switched to `Promise.allSettled` for parallel processing, ensuring that one failed email (timeout, OpenAI rate limit) doesn't wipe out the results of the other emails in the same batch — unlike `Promise.all`, which rejects the entire batch if even a single item fails.

**5. `connectionId` was hard-cached at the UI layer, out of sync with the connection's real state.** This was the deepest and hardest-to-spot root cause in the entire debugging process: the Home screen stored `connectionId` in its state only once, at initialization. When the WebSocket connection dropped (due to a network change, a lost connection, or the OS suspending a background connection), the underlying service cleared its internal value to `null`, but the screen's state was never updated to match — resulting in a dead `connectionId` being sent to the server. The backend returned a `410 Gone` error when trying to push the result, but because this failure happened server-side, after the REST call had already returned successfully, the user saw no error message at all — just a spinner that never resolved.

Evidence confirming the cause: the `ws-disconnect` Lambda's logs showed the connection had closed *before* the user tapped Check Gmail, not during processing. The fix: read `connectionId` directly from the service (the live source of truth) at the exact moment of use, instead of trusting the cached value in state, and automatically reconnect if that value turns out to be `null`.

#### Contents

{{% children /%}}

#### Outcomes of this section

- A complete Flutter app running on a real Android device (Samsung S23 Ultra), with an instance-based architecture across the entire client service layer
- The Cognito sign-in flow, Gmail OAuth deep link, and real-time WebSocket connection all run reliably end-to-end
- A `whoami` route added to the WebSocket API to safely obtain the `connectionId`, independent of `$connect`
- The Worker processes emails in parallel with per-item fault tolerance, instead of losing the whole batch over one failure
- Identified and fixed a subtle class of bug: cached connection state at the UI layer drifting out of sync with the network connection's actual state — a lesson that applies to any real-time application, not just WebSocket
