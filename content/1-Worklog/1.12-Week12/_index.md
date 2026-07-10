---
title: "Worklog Week 12"
date: 2026-07-92
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Week 12 Objective: The week of "invisible" bugs — end-to-end integration debugging

The backend was completed last week, and the team member's Flutter app is also built — theoretically, it's just "plug and play." In reality, this week became the most intense debugging week of the entire project: a series of cascading errors at the exact integration points between components, while each individual component "seemed fine." As the person in charge of the backend and architecture, I was the primary tracer for these cross-tier bugs.

- Supported the Flutter member in end-to-end testing on a real Android device, tracing WebSocket integration errors.
- Resolved the issue where the `whoami` route returned `Forbidden` even though all resources reported successful creation.
- Traced and handled the `410 GoneException` error when the Worker pushed results — the problem of a "dead" `connectionId` that nobody knew about.
- Optimized the Worker: shifted email processing from sequential to parallel, with element-wise fault tolerance.
- Summarized all used services, compared actual costs with the Free Tier, and finalized the architecture documentation for the report.

---

### Tasks to implement this week:

| Day | Task Category | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Monday | - Work with the Flutter member to run the first end-to-end test on a real device. <br> - Note the phenomenon: app reports "WebSocket not ready", `whoami` request receives `{"message": "Forbidden"}`. | 22/06/2026 | 22/06/2026 | Internal project |
| Tuesday | - Trace the Forbidden error: check CloudWatch Logs of the `ws-whoami` Lambda, discover the log group never existed → request never reached the Lambda. <br> - Check CloudFormation: all whoami resources are `CREATE_COMPLETE`. Check API Gateway Stages: discover the `prod` stage is still pointing to an older deployment prior to the route's creation date. | 23/06/2026 | 23/06/2026 | https://docs.aws.amazon.com/apigateway/ |
| Wednesday | - Manually deploy the API to the `prod` stage to publish the new route, verify whoami works. <br> - Research documentation: confirm `AWS::ApiGatewayV2::Deployment` does not automatically create a new version when routes change, even with `DependsOn` — noted as a lesson learned for the report. | 24/06/2026 | 24/06/2026 | https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-apigatewayv2-deployment.html |
| Thursday | - New incident: Check Gmail runs but the app receives no results. Worker log reports `WebSocket push failed: GoneException (410)`. <br> - Add detailed logs (`err.name`, `$metadata.httpStatusCode`) to the Worker's push function, redeploy to gather diagnostic data. | 25/06/2026 | 25/06/2026 | https://docs.aws.amazon.com/apigateway/ |
| Friday | - Compare timestamps between the `ws-disconnect` log and the Worker log: discover the connection was closed **before** the user tapped the button — the app is sending an old, dead `connectionId`. <br> - Work with the Flutter member to identify the root cause at the UI layer (state cache `connectionId` is out of sync with real connection status) and the fix (read fresh value + auto reconnect). | 26/06/2026 | 26/06/2026 | Internal project |
| Saturday | - Optimize Worker: change the sequential OpenAI calling loop to `Promise.allSettled` — process in parallel, one failed email doesn't drop the results of other emails. <br> - Retest end-to-end: summary results successfully display on the real app via WebSocket push. | 27/06/2026 | 27/06/2026 | https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/allSettled |
| Sunday | - Compile a service lookup table (service – role – reason for selection – risks) for the entire architecture. <br> - Cross-check the Billing Dashboard, confirm costs are within the Free Tier + OpenAI costs are minimal. <br> - Write the weekly summary report and handover documents for the member in charge of writing docs. | 28/06/2026 | 28/06/2026 | Internal InboxIQ project |

---

### Week 12 Achievements:

#### 1. The biggest lesson: "successfully created" does not mean "currently running"

The `whoami` route returning `Forbidden` incident was the most valuable lesson about CloudFormation and API Gateway. All normal check layers reported fine: `sam deploy` succeeded, CloudFormation logged `CREATE_COMPLETE` for all 4 resources, and the route fully displayed in the Console. But the `prod` stage was still running an **old deployment** from before the route existed — because `AWS::ApiGatewayV2::Deployment` only creates a new version when the resource itself changes properties, and `DependsOn` only ensures creation order; it doesn't force a re-deploy.

Key tracing technique: checking **if the destination Lambda's log group exists**. A log group is only created when the Lambda runs for the first time — "log group does not exist" is absolute proof that the request never touched the function, immediately isolating the bug to the routing layer instead of wasting time doubting the code.

#### 2. Tracing the 410 Gone error by timestamp comparison — debugging like an investigation

The second error was much more subtle because it was completely "silent": the user taps the button, all APIs return success, but the results never appear. The Worker log showed the push failed with `410 GoneException` — the connection no longer existed. The question was: when did it die, and why was the app still using it?

Solution method: place the logs from three sources (`ws-disconnect`, the button tap time inferred from `jobId`, Worker log) on the same timeline. The result was clear as day — the connection had closed 18 seconds **before** the user tapped the button. The issue wasn't on the backend: the app was holding an old `connectionId` in the screen's state, failing to sync when the real connection dropped. From this diagnosis, the Flutter member fixed it in the right place (reading a "fresh" `connectionId` from the service at the time of use, auto-reconnecting if null) instead of blindly guessing.

Methodological lesson: in a multi-component asynchronous system, **timestamps are the most powerful diagnostic tool** — many bugs only reveal their true form when events are lined up on the same timeline.

#### 3. `Promise.allSettled` — element-wise fault tolerance instead of "all or nothing"

The first version of the Worker called OpenAI sequentially for each email — time increased linearly with the number of emails, and one failed email ruined the whole batch. Switching to `Promise.allSettled`: emails are processed in parallel (total time ≈ slowest email instead of cumulative sum), and any failed email is isolated, while successful emails still return results normally. The difference from `Promise.all` (rejecting the whole batch when one element fails) is an important detail to articulate clearly during the report defense.

#### 4. Complete end-to-end system on a real device

By the end of the week, the full chain was verified: user taps Check Gmail on a real Android app → Producer → SQS → Worker (Gmail + OpenAI in parallel) → DynamoDB → WebSocket push → summary list appears on the screen within seconds. The entire development cost remains within the AWS Free Tier, plus negligible OpenAI costs.

---

### Week 12 Outcome Evaluation:

- Thoroughly resolved the two most difficult integration bugs of the project (unpublished route, dead `connectionId`) using a systematic tracing method instead of trial and error.
- Optimized the Worker in both speed (parallel processing) and durability (element-wise fault tolerance).
- The system runs completely end-to-end on a real device — the main technical goal of the entire group project has been achieved.
- Completed the service lookup table and cost metrics, handing them over to the documentation member to include in the final team report.

---

### Difficulties encountered:

- Both major bugs of the week were literally "invisible":