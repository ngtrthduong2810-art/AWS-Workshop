---
title: "Worklog Week 9"
date: 2026-06-09
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objective: Reviewing the architecture through the lens of a "service user" rather than a "code writer"

After many weeks focusing on writing code, fixing bugs, and running tests for the InboxIQ project, week 9 is the time to pause to **synthesize and re-examine the core nature of each AWS service actually implemented in the product**. The goal is not to learn a new service, but to deeply understand *why* each service was chosen, what manual process it replaces, and what its limitations/risks are. This is an important preparation step for the thesis defense, as the examiners will undoubtedly ask "why use X instead of Y".

- Review the entire 5 architectural layers of InboxIQ (User, Backend, Workflow, Storage, Monitoring) and exactly list which services are currently running in the account.
- Deeply understand the role of Amazon Cognito in user authentication, comparing it with the alternative of manually building a JWT system.
- Analyze the reasons for separating into two Lambdas (Producer/Worker) and an auxiliary Lambda (ws-whoami) instead of combining all logic into a single function.
- Clearly understand the mechanism of Amazon API Gateway in both REST and WebSocket modes, as it is a service rarely used simultaneously in both modes for a student project.
- Delve into the "buffer" role of Amazon SQS and Dead-Letter Queue in decoupling the processing speed of the client and the AI.
- Review the design of the 6 DynamoDB tables, especially the strategy of using TTL to automatically clean up data instead of writing manual cron jobs for deletion.
- Understand why sensitive information (OpenAI key, Gmail OAuth secret) is isolated into Secrets Manager and SSM Parameter Store rather than being left in Lambda environment variables.
- Review the monitoring roles of CloudWatch and X-Ray in tracing a request traversing multiple asynchronous Lambdas.
- Cross-check all used services against actual Free Tier costs, preparing data for the "estimated cost" section of the report.

---

### Tasks to implement this week:

| Day | In-depth task category | Start Date | End Date | Reference materials |
| --- | --- | --- | --- | --- |
| Monday | - Redraw the 5-layer architecture diagram on paper, cross-checking each block with real resources in the AWS Console. <br> - Re-read the official documentation on Amazon Cognito User Pool: registration, login, and JWT issuance flows. <br> - Compare with how the Flutter `AuthService` calls Cognito directly. | 22/06/2026 | 22/06/2026 | https://docs.aws.amazon.com/cognito/ |
| Tuesday | - Research AWS Lambda documentation regarding execution time limits, cold starts, and concurrency. <br> - Analyze the reasoning for splitting Producer/Worker: Producer only returns a fast `202 Accepted`, while Worker handles heavy processing (calling Gmail + OpenAI) running in the background. <br> - Understand why a separate `ws-whoami` Lambda is needed for the WebSocket route. | 23/06/2026 | 23/06/2026 | https://docs.aws.amazon.com/lambda/ |
| Wednesday | - Research Amazon API Gateway documentation: differences between REST API and WebSocket API. <br> - Research the WebSocket connection lifecycle (`$connect`, `$disconnect`, custom route) and why `$connect` cannot push messages. <br> - Compare the Lambda Authorizer with authenticating JWTs on each REST request. | 24/06/2026 | 24/06/2026 | https://docs.aws.amazon.com/apigateway/ |
| Thursday | - Research Amazon SQS: Standard Queue, Visibility Timeout, redrive policy, and Dead-Letter Queue. <br> - Understand Partial Batch Response for the SQS-Lambda trigger, and why it prevents reprocessing an entire batch when only 1 message fails. <br> - Understand Amazon EventBridge Scheduler and the cron-based invoke model. | 25/06/2026 | 25/06/2026 | https://docs.aws.amazon.com/sqs/ <br> https://docs.aws.amazon.com/eventbridge/ |
| Friday | - Review DynamoDB table design: Partition Key, Sort Key, Global Secondary Index (if any), and the TTL mechanism for auto-deleting data. <br> - Cross-reference the 6 actual tables (`users`, `user-settings`, `gmail-connections`, `email-summaries`, `processing-jobs`, `ws-connections`) with the intended purpose of each table. <br> - Confirm which tables are actually being read/written in the code, and which are only declared in the SAM template. | 26/06/2026 | 26/06/2026 | https://docs.aws.amazon.com/dynamodb/ |
| Saturday | - Understand AWS Secrets Manager and Systems Manager Parameter Store: when to use which, and how their costs differ. <br> - Research the mechanism of caching secrets at the global scope in Lambda to avoid calling Secrets Manager on every invoke (reducing cost + latency). <br> - Review CloudWatch Logs/Metrics and AWS X-Ray tracing across asynchronous Lambdas. | 27/06/2026 | 27/06/2026 | https://docs.aws.amazon.com/secretsmanager/ <br> https://docs.aws.amazon.com/xray/ |
| Sunday | - Synthesize all used services into a quick reference table (service – role – what it replaces – risks). <br> - Cross-check with Cost Explorer/Billing Dashboard to verify actual cost metrics within the Free Tier. <br> - Write the weekly summary report: achievements, difficulties, solutions, and lessons learned. | 28/06/2026 | 28/06/2026 | Internal InboxIQ project documents |

---

### Week 9 Achievements: Lookup Map of Services Applied to InboxIQ

#### 1. Authentication Layer — Amazon Cognito

Stepping back to learn about Cognito after finishing its integration helped me better understand *why* it is more worthwhile than writing a custom JWT system. Cognito User Pool handles the entire lifecycle: registration, email verification, login, and issuing/refreshing JWTs, without me having to manually store passwords or handle hashing. In the Flutter app's `AuthService`, calling Cognito directly (bypassing API Gateway) is a logical choice because Cognito already exposes a secure authentication endpoint inherently — API Gateway only needs to verify the JWT at the backend business APIs (Producer). This was a point I had mistakenly documented in last week's architecture notes and have now corrected to match the actual code.

#### 2. Compute Layer — AWS Lambda (Producer / Worker / ws-whoami)

Re-reading the Lambda documentation helped me clearly articulate the decision to split into 3 functions instead of 1:

- **Lambda Producer**: does only one thing — receives the request, packages the message with `connectionId`, pushes it to SQS, and immediately returns `202 Accepted`. This keeps the API response time extremely short, preventing client-side timeouts.
- **Lambda Worker**: handles heavy processing (calling Gmail API, calling OpenAI, writing to DynamoDB, pushing to WebSocket), and is triggered asynchronously from SQS, so it can run longer than the timeout limit of a standard API Gateway request without affecting the user experience.
- **Lambda ws-whoami**: stems from a practical limitation of API Gateway WebSocket — the `$connect` route does not guarantee the ability to push messages back to the client immediately upon connection. Separating a distinct route for the app to proactively request the `connectionId` is an architectural solution true to its nature, not a temporary patch.

Splitting into 3 Lambdas also aligns with the IAM Least Privilege principle: each function is granted exactly the necessary permissions (Producer does not need permissions to call Gmail/OpenAI, and Worker does not need permissions to write to SQS Main aside from receiving triggers).

#### 3. Entry Gateway Layer — Amazon API Gateway (REST + WebSocket)

This is the service that surprised me the most when re-reading the docs, because most student projects only use either REST or WebSocket modes, whereas InboxIQ uses both for two different purposes:

- **REST API**: receives the "Check Gmail" request — a classic request/response model, suitable because the client initiates the action proactively.
- **WebSocket API**: used to push AI processing results back to the app in real-time, because AI processing takes anywhere from a few seconds to tens of seconds — using continuous REST polling would consume more resources and lead to a much chunkier user experience.

The Lambda Authorizer authenticates JWTs at the REST layer, completely separating the authentication logic from the business logic within the Producer.

#### 4. Asynchronous Workflow Layer — Amazon SQS and EventBridge

Re-reading the SQS documentation helped me accurately articulate why the system is more stable with a queue in the middle: SQS acts as a "buffer," decoupling the incoming request rate (which can be sudden and massive) from the processing rate the Worker can handle (limited by OpenAI/Gmail rate limits). The **Partial Batch Response** mechanism is particularly important — when the Worker processes a batch of multiple messages, if only one message fails, SQS will retry only that specific message instead of the entire batch, avoiding unnecessary duplicate processing. After 3 failed retry attempts, the message automatically moves to the Dead-Letter Queue to prevent it from getting stuck in the main queue forever.

EventBridge Scheduler plays an optional role — periodically pushing messages (every 30 minutes) to the SQS Main queue exactly like a real user request, instead of triggering the Worker directly. This design ensures both flows (manual and automated) pass through the exact same single entry point, reducing the risk of having two different processing logic paths for the same task.

#### 5. Storage Layer — Amazon DynamoDB (6 tables)

Reviewing the 6 tables made me clearly realize that the strategy of using **TTL (Time To Live)** to automatically clean up data was a significant effort-saving decision — there's no need to write a Lambda cron job to delete old data; DynamoDB automatically deletes items when they expire:

| Table | Role | TTL |
|---|---|---|
| `inboxiq-users` | Basic user information | None |
| `inboxiq-user-settings` | Personalization settings | None |
| `inboxiq-gmail-connections` | Store Gmail OAuth token | None |
| `inboxiq-email-summaries` | Email summaries | 30 days |
| `inboxiq-processing-jobs` | Processing status (debug) | 7 days |
| `inboxiq-ws-connections` | Mapping connectionId ↔ userId | 2 hours |

An important point to note and be honest about during the defense: the `inboxiq-processing-jobs` table is currently only declared in the SAM template, and there is no code actually writing data to it yet — it must be clearly stated that this is a backup table for debugging in a later phase, not a completed feature.

#### 6. Configuration Security Layer — Secrets Manager and SSM Parameter Store

Re-reading the documentation helped me clearly distinguish when to use which service: **Secrets Manager** is used for truly sensitive data that requires rotation (OpenAI API key), while **SSM Parameter Store** is suitable for less sensitive configurations or those not requiring auto-rotation, at a significantly lower cost. Caching secrets at the **global scope** of the Lambda (outside the handler function) is a crucial technical detail — it allows the secret to be fetched only once when the Lambda container starts up (cold start); subsequent invocations reusing the container will reuse the cached value, simultaneously reducing latency and the number of API calls to Secrets Manager (which charges per API call).

#### 7. Monitoring Layer — CloudWatch and X-Ray

Since the system involves multiple Lambdas calling each other asynchronously via SQS and WebSockets, debugging a specific request (e.g., why an email wasn't summarized) cannot rely solely on the logs of a single function. CloudWatch Logs stores detailed logs for each Lambda, while X-Ray allows stitching trace segments together into a cohesive "journey" spanning Producer → SQS → Worker → DynamoDB/WebSocket, helping to pinpoint exactly which step was delayed or failed instead of just guessing.

---

### Practical Experience: Cross-checking documentation with the real system

**Module 1 — Checking the authentication layer**
- Open the AWS Console and navigate to the Cognito User Pool used for InboxIQ.
- Check the App Client, confirming that the client secret is not enabled (which is mandatory for mobile app public clients).
- Cross-check the `InitiateAuth` flow in `AuthService` against the official Cognito documentation.

**Module 2 — Checking the compute layer**
- Open the Lambda Console and navigate to Producer, Worker, and ws-whoami one by one.
- Check the IAM Role attached to each function, confirming adherence to the Least Privilege principle (each function only has permissions corresponding to its role).
- Review the timeout and memory configurations for each function, matching them with their task characteristics (Producer has a short timeout, Worker has a longer timeout).

**Module 3 — Checking the entry gateway layer**
- Navigate to the API Gateway Console, check the REST route (`/check-gmail`) and WebSocket routes (`$connect`, `$disconnect`, `whoami`).
- Verify that the Lambda Authorizer is correctly attached to the REST route that requires authentication.

**Module 4 — Checking the workflow layer**
- Go to the SQS Console, check the Main Queue and Dead-Letter Queue, and review the redrive policy (maxReceiveCount = 3).
- Open the EventBridge Console, check that the Scheduler rule correctly points to the SQS Main Queue.

**Module 5 — Checking the storage layer**
- Open the DynamoDB Console, inspect each of the 6 tables, and verify if the TTL configuration is enabled on the correct field.
- Run a test query on the `inboxiq-email-summaries` table to confirm that actual data is being written with the correct structure.

**Module 6 — Checking the configuration security and monitoring layer**
- Access Secrets Manager and verify that the OpenAI key is stored in the correct location and is not present in Lambda environment variables in plaintext.
- Open CloudWatch Logs Insights and run a test query filtering logs by `connectionId` to confirm the ability to trace a specific request.
- Open the X-Ray Service Map and verify visibility of the pathway between the Producer, SQS, and Worker.

---

### Week 9 Outcome Evaluation:

- Built a complete "lookup map": service – role – reason for selection – risks, covering all 5 architectural layers of InboxIQ.
- Solidified the technical reasoning behind each design decision, ready to answer "why use X" questions during the report defense.
- Discovered and honestly documented an incomplete aspect: the `inboxiq-processing-jobs` table only exists at the infrastructure level and lacks data-writing logic.
- Clarified the differences between Secrets Manager and SSM Parameter Store, applying the right service for the right type of data.
- Reconfirmed that actual costs remain within the Free Tier + OpenAI API costs are as low as initially estimated.

---

### Difficulties encountered during the review process:

- Some old architectural notes (written last week) did not fully match the actual code — for example, incorrectly describing the flow of the App calling Cognito via API Gateway, when in reality, the App calls Cognito directly.
- Distinguishing exactly when to use Secrets Manager vs. SSM Parameter Store was difficult just by reading docs without cross-checking the actual costs of each service.
- Tracing an asynchronous request across multiple Lambdas using X-Ray required a clear understanding of trace segment/subsegment concepts, which was initially confusing as I was used to looking at the linear logs of a single function.
- Realizing a DynamoDB table (`inboxiq-processing-jobs`) was declared but unused, which could easily cause misunderstandings if not carefully checked before writing the report.

---

### Solutions and Best Practices derived:

- Always cross-check architectural documents with the Console/real code before including them in the final report, instead of fully trusting old notes.
- Clearly state the actual status of each resource (in use / newly declared / backup) rather than assuming everything in the SAM template is actively running.
- When comparing two similar services (Secrets Manager vs. SSM Parameter Store), create a concise comparison table based on criteria: cost, rotation capability, and appropriate sensitivity level.
- Practice reading the X-Ray Service Map more frequently instead of relying solely on CloudWatch Logs, to get used to tracing asynchronous systems.
- Maintain the habit of regularly checking the Billing Dashboard even if the system is on the Free Tier, to quickly detect any services incurring unexpected costs.

---

### Optimization directions for the next week:

- Add actual logic to write data into the `inboxiq-processing-jobs` table, or consider removing it from the architecture if it is unnecessary for the MVP.
- Learn more about AWS Cost Explorer to perform detailed cost analysis for each service in InboxIQ, serving the "estimated cost" section of the graduation report.
- Consider adding `WidgetsBindingObserver` on the Flutter side to automatically reconnect WebSockets when the app resumes, instead of only reconnecting when the user taps a button.
- Review the feasibility of upgrading the Lambda runtime from Node.js 20.x (which is EOL) to a newer version before submitting the final report.
- Prepare slides and comparative cost data between "self-hosted" and "using AWS managed services" for each layer, to be used in the project defense presentation.