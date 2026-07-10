---
title: "Worklog Week 11"
date: 2026-06-25
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objective: Real-time System Implementation — API Gateway WebSocket and Gmail Integration in Worker

Last week, the system was able to run with mock messages and the results were sitting statically in DynamoDB. This week has two major goals: first, integrate the Gmail OAuth portion (completed by the member in charge of security) into the Worker to summarize real emails; second — and much more difficult — build a WebSocket channel to push results back to the app in real-time instead of forcing the app to constantly poll. This is the week I had to read the most API Gateway documentation since the start of the project, as the WebSocket API operates on a completely different model compared to the familiar REST API.

- Integrate the Gmail API into the Worker: read the OAuth token from DynamoDB, automatically refresh when the token expires (using a shared Lambda Layer written by the OAuth member).
- Set up the API Gateway WebSocket with `$connect` and `$disconnect` routes, along with a Lambda Authorizer to authenticate JWTs via query strings.
- Design the `inboxiq-ws-connections` table to store the `connectionId` ↔ `userId` mapping so the Worker knows who to push results to.
- Write the push logic from the Worker to the client via `PostToConnectionCommand`.
- Solve the problem of "how the client knows its own connectionId" — leading to the decision to add a dedicated `whoami` route.
- Update `template.yaml` for all WebSocket resources, maintaining the Infrastructure as Code principle.

---

### Tasks to implement this week:

| Day | Task Category | Start Date | End Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Monday | - Receive the `gmail-shared` Lambda Layer (the `refreshAccessToken` function) from the OAuth member. <br> - Integrate into Worker: read token from `inboxiq-gmail-connections` table, check `expiresAt`, automatically refresh when expired. | 15/06/2026 | 15/06/2026 | Internal team + https://developers.google.com/gmail/api |
| Tuesday | - Write the `fetchUnreadEmails` function in the Worker: call Gmail API to fetch the list of unread emails with metadata (Subject, From, Date), using an AbortController for timeout limits. <br> - First end-to-end test with a real Gmail inbox: Producer → SQS → Worker → Gmail → OpenAI → DynamoDB. | 16/06/2026 | 16/06/2026 | https://developers.google.com/gmail/api |
| Wednesday | - Study API Gateway WebSocket documentation: route selection model (`$request.body.action`), `$connect`/`$disconnect` lifecycle, and how the backend proactively pushes via the Management API. <br> - Create the `inboxiq-ws` WebSocket API in `template.yaml`. | 17/06/2026 | 17/06/2026 | https://docs.aws.amazon.com/apigateway/ |
| Thursday | - Write the Lambda Authorizer to authenticate the Cognito JWT passed via the `?token=` query string during `$connect` (WebSockets cannot send custom headers from browser/mobile). <br> - Write the `ws-connect` Lambda (save `connectionId` + `userId` to the table with a 2-hour TTL) and `ws-disconnect` (delete the record upon disconnection). | 18/06/2026 | 18/06/2026 | https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html |
| Friday | - Write push logic in the Worker: initialize `ApiGatewayManagementApiClient` with an `https://` endpoint (not `wss://`), call `PostToConnectionCommand` to send the payload `{type: "summary-ready", summaries: [...]}`. <br> - Wrap the push call in a separate try/catch block so a push error doesn't crash the entire processing batch. | 19/06/2026 | 19/06/2026 | https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-how-to-call-websocket-api-connections.html |
| Saturday | - Solve the problem of the client needing to know its `connectionId`: research and confirm that the `$connect` handler should not push messages immediately (due to the risk of a `GoneException` since the connection may not be fully "alive" at that exact moment). <br> - Design a dedicated `whoami` route: the client proactively sends `{"action": "whoami"}`, and the `ws-whoami` Lambda returns the `connectionId` over that same connection. | 20/06/2026 | 20/06/2026 | https://docs.aws.amazon.com/apigateway/ |
| Sunday | - Finalize `template.yaml`: add `WsWhoamiFunction`, `WhoamiRoute`, `WhoamiIntegration`, and the corresponding Lambda Permissions. <br> - Run `sam build && sam deploy`, check the changeset. <br> - Test WebSocket push using `wscat` from the local machine, hand over the message format to the Flutter member. | 21/06/2026 | 21/06/2026 | Internal InboxIQ project |

---

### Week 11 Achievements:

#### 1. The Worker successfully summarized real emails

The most memorable moment of the week: querying the `inboxiq-email-summaries` table for the first time and seeing real emails from an inbox fully analyzed by GPT-4o-mini — featuring Vietnamese summaries, classification (work/promo/notification), priority scoring, and action suggestions. The Gmail token integration flow (reading from DynamoDB, auto-refreshing via the shared Layer) worked smoothly thanks to the clear boundaries set last week: the OAuth member handles fetching and saving the token, and I only need to "consume" it correctly.

#### 2. WebSocket API — a completely different mental model from REST

The realization I had when reading the docs: API Gateway's WebSocket API is not just a "long-lived REST API"; it's an entirely different model. There are no URL paths — instead, there is a **route selection expression** (`$request.body.action`): API Gateway reads the `action` field in the JSON body of the message to decide which route handles it. For the backend to proactively send a message to the client, it must go through a separate Management API with an `https://` endpoint and a `connectionId` — it does not simply "reply" directly like a REST response.

A crucial security detail to remember: WebSocket handshakes from mobile/browsers cannot attach custom headers, so the JWT must be passed via a **query string** and authenticated by the Lambda Authorizer exactly at the `$connect` phase — doing this once for the entire lifecycle of the connection, unlike REST which authenticates every single request.

#### 3. The `whoami` route — an architecturally sound solution rather than a patch

A seemingly small problem turned out to be an important design decision: the Worker needs the `connectionId` to push data, but the client doesn't inherently know its own `connectionId`. The first thought was to have the `$connect` handler immediately push a "welcome" message containing the ID — but documentation and testing showed that at the time the `$connect` handler runs, the connection isn't guaranteed to be fully "alive", and pushing immediately risks a flaky `GoneException` that is hard to reproduce.

The chosen solution: a custom `whoami` route — after the connection is stable, the client proactively sends `{"action": "whoami"}` and the Lambda returns the `connectionId` over that exact connection. This turns an unpredictable sequence ("when will the server push?") into a deterministic sequence controlled by the client ("the client asks when it is ready").

#### 4. Push errors must not break the entire batch

The `PostToConnectionCommand` call is wrapped in its own try/catch block, only logging a warning on failure (e.g., if the client disconnected) — because the summary results are already safely stored in DynamoDB, the push is merely a "notification", and a failed push does not mean a failed job. If the push error were thrown outwards, the message would be retried by SQS, and OpenAI would be called again pointlessly, leading to double billing.

---

### Week 11 Outcome Evaluation:

- The complete pipeline with real data: Gmail → OpenAI → DynamoDB is running stably, confirmed by multiple tests.
- The entire WebSocket infrastructure (API, Authorizer, 3 routes, connection mapping table) has been fully declared in SAM and deployed.
- The `whoami` route was designed and implemented as a grounded architectural decision, not a hack — the reasoning was clearly documented in the design docs for the thesis defense.
- Handed over the WebSocket message formats (`whoami-response`, `summary-ready`) to the Flutter member, along with instructions on passing the JWT via the query string.

---

### Difficulties encountered:

- Initial confusion regarding the Management API endpoint: I assumed pushing also used `wss://` like the client connection, but it turns out the backend must call it via `https://` — using the wrong protocol fails immediately, but the error message doesn't clearly state the cause.
- The Lambda Authorizer for WebSockets has a different event structure than the REST API Authorizer; copying the REST boilerplate code over resulted in silent failures.
- Spent a lot of time weighing the two options for retrieving the `connectionId` (`$connect` pushing welcome vs. a dedicated `whoami` route) — the lesson here is that "small" decisions at the protocol layer often take more time to think through than writing the actual code.

---

### Solutions and Best Practices derived:

- For API Gateway WebSockets, remember the rule: the client connects via `wss://`, while the backend pushes via `https://` using the Management API — two different "faces" of the same API.
- Read the documentation carefully for the sample event structures for each type of Authorizer (REST vs. WebSocket vs. HTTP API) instead of blindly reusing code between them.
- Document the reasoning behind every design decision exactly when it is made (even if just a few lines) — a week later, you won't remember why you chose one option over the other.

---

### Directions for the next week:

- Coordinate with the Flutter member for end-to-end testing on real devices: the app connects to the WebSocket, sends `whoami`, taps "Check Gmail", and receives the pushed results.
- Prepare mentally to debug integration issues — experience shows that connecting components written by different people always uncovers unforeseen bugs.
- Review the entire architecture and prepare cost metrics and a service lookup table for the final report.