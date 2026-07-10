---
title: "Worklog Week 10"
date: 2026-06-16
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objective: Laying the serverless architecture foundation for InboxIQ

This week marks the kickoff for the backend of the InboxIQ group project — an AI-powered email categorization system built on a serverless architecture. Taking the role in charge of the backend and overall architecture, my goal is to build the "backbone" of the system: transforming the architectural diagram on paper into real resources running in the AWS account, ready for other team members to plug their respective parts (Flutter app, Gmail OAuth) into in the upcoming weeks.

- Finalize the 5-layer architecture diagram (User, Backend, Async Workflow, Storage, Monitoring) with the whole team, defining the boundaries of each person's tasks.
- Set up the storage infrastructure: design and create DynamoDB tables with a TTL strategy for automatic data cleanup.
- Set up the SQS Main queue alongside a Dead-Letter Queue with a redrive policy, acting as a "buffer" between user requests and AI processing.
- Write two core Lambdas following the Producer/Worker model: the Producer receives requests and returns a fast response, while the Worker handles heavy background processing via an SQS trigger.
- Bring the entire infrastructure under AWS SAM (Infrastructure as Code) management, instead of manually creating each resource in the Console.
- Integrate the OpenAI API (GPT-4o-mini) call within the Worker to summarize and categorize emails, storing the key in Secrets Manager with a caching mechanism at the global scope.

---

### Tasks to implement this week:

| Day | Task Category | Start Date | End Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Monday | - Team meeting to finalize the 5-layer architecture and assign roles: I take the backend + architecture, member A takes Flutter, member B takes OAuth/security, and member C takes documentation/testing. <br> - Draw a detailed architecture diagram on draw.io, numbering each processing flow. | 08/06/2026 | 08/06/2026 | Internal team |
| Tuesday | - Design the DynamoDB table schemas: partition key, sort key, and TTL field for each table. <br> - Create the `inboxiq-email-summaries` (30-day TTL), `inboxiq-gmail-connections`, `inboxiq-ws-connections` (2-hour TTL), and `inboxiq-processing-jobs` (7-day TTL) tables. | 09/06/2026 | 09/06/2026 | https://docs.aws.amazon.com/dynamodb/ |
| Wednesday | - Create the SQS Main Queue and Dead-Letter Queue, configure the redrive policy maxReceiveCount = 3. <br> - Understand Visibility Timeout and its relationship with the Lambda Worker's timeout to avoid duplicate message processing. | 10/06/2026 | 10/06/2026 | https://docs.aws.amazon.com/sqs/ |
| Thursday | - Initialize the SAM project, write the first version of `template.yaml`: declare the Producer, Worker, and SQS trigger with Partial Batch Response. <br> - Write the Lambda Producer: receive the request along with `connectionId`, package the message and push it to SQS, returning `202 Accepted` immediately. | 11/06/2026 | 11/06/2026 | https://docs.aws.amazon.com/serverless-application-model/ |
| Friday | - Write the skeleton for the Lambda Worker: receive the batch from SQS, parse messages, and handle errors using the `batchItemFailures` model. <br> - Create the `inboxiq/openai-api-key` secret in Secrets Manager, write a function to fetch the key with a cache at the Lambda's global scope. | 12/06/2026 | 12/06/2026 | https://docs.aws.amazon.com/secretsmanager/ |
| Saturday | - Integrate the OpenAI API (GPT-4o-mini) call into the Worker: prompt for summarizing Vietnamese emails, returning JSON containing summary/priority/category/action. <br> - Write a function to save results to DynamoDB including the `expireAt` TTL field. | 13/06/2026 | 13/06/2026 | https://platform.openai.com/docs/ |
| Sunday | - Run `sam build && sam deploy` for the first time, check the changeset, and verify that the entire `inboxiq-backend` stack was successfully created. <br> - Test the Producer → SQS → Worker → DynamoDB flow using mock messages (no real Gmail yet). <br> - Write the weekly summary report, hand over endpoints and message structures to member A (Flutter) and member B (OAuth). | 14/06/2026 | 14/06/2026 | Internal InboxIQ project |

---

### Week 10 Achievements:

#### 1. The overall architecture is finalized and becomes the team's shared "contract"

The 5-layer diagram is not just a drawing for the report — it has become an actual task assignment document: every member can look at it and know exactly where their boundaries are and their integration points with others' parts (for example: member A only needs to know that the Producer receives a JSON body containing a `connectionId` and returns a `202`, without worrying about how the Worker processes it). Finalizing this "communication contract" early helps the entire team work in parallel without stepping on each other's toes.

#### 2. Producer/Worker model — the most important architectural decision of the week

Initially, I intended to write a single Lambda to handle everything, but when calculating the time: calling the Gmail API (a few seconds) + calling OpenAI for multiple emails (potentially tens of seconds) would far exceed a reasonable timeout for an API Gateway request, leaving the user staring at a frozen screen for a long time. Separating it into a Producer (instant response) and a Worker (background processing via SQS) completely solves this problem. SQS in the middle also acts as a "buffer": if many users tap the button simultaneously, requests queue up waiting for the Worker to process them gradually rather than overloading the system.

#### 3. Partial Batch Response — a small detail that saves the whole batch

When the Worker receives a batch of multiple messages from SQS, if only one message fails and returns an error for the entire batch, SQS will retry everything — including the successfully processed messages, causing duplicate summaries and wasting OpenAI API costs. Configuring `FunctionResponseTypes: ReportBatchItemFailures` along with returning `batchItemFailures` that contain only the failed messages allows SQS to retry exactly the broken parts. After 3 failed attempts, messages drop into the Dead-Letter Queue to avoid clogging the main queue.

#### 4. DynamoDB TTL — replacing an entire cron job

Designing the `expireAt` field (Unix timestamp) for each table allows DynamoDB to automatically delete expired data: email summaries disappear on their own after 30 days, and WebSocket connection mappings clean themselves up after 2 hours. There is no need to write any additional periodic Lambdas for garbage collection — a prime example of "letting a managed service do its job".

#### 5. Caching secrets at the global scope — saving both latency and costs

Secrets Manager charges per API call. Placing the cache variable outside the handler function ensures the key is only retrieved once when the Lambda container starts up (cold start); subsequent invokes on the same container reuse the cached value. It's a small detail but exactly follows best practices for every Lambda requiring a secret.

---

### Week 10 Outcome Evaluation:

- The entire backend infrastructure layer (DynamoDB, SQS, Lambda Producer/Worker, Secrets Manager) is actually running in the account, fully managed by SAM.
- The asynchronous flow Producer → SQS → Worker → DynamoDB has been verified with mock messages, ready to integrate with real Gmail once member B finishes OAuth.
- Handed over clear "communication contracts" (message format, endpoints) to the two members handling Flutter and OAuth, paving the way for parallel work starting in week 8.

---

### Difficulties encountered:

- When writing `template.yaml` for the first time, it's easy to confuse the properties of `AWS::Serverless::Function` (SAM) and `AWS::Lambda::Function` (pure CloudFormation) — the syntaxes are similar but not interchangeable.
- Determining an SQS Visibility Timeout that matches the Worker's timeout is not straightforward: setting it too short causes duplicate processing while the Worker is still running, while setting it too long means failed messages have to wait a long time before being retried.
- The prompt for GPT-4o-mini had to be tweaked many times to return stable JSON — initially, the model occasionally included conversational filler outside the JSON, causing parsing errors.

---

### Solutions and Best Practices derived:

- Read the SAM documentation carefully regarding "resource types" before writing the template, cross-checking every property against the docs instead of guessing based on feeling.
- Set the SQS Visibility Timeout to be larger than the Lambda Worker's timeout (officially recommended to be ~6 times larger) to ensure the Worker finishes before the message can reappear.
- Use the `response_format: json_object` parameter in the OpenAI API to force the model to only return JSON, combined with explicitly stating the desired schema directly in the system prompt.

---

### Directions for the next week:

- Coordinate with member B to integrate the Gmail OAuth token into the Worker: read the token from DynamoDB and handle token refreshing when it expires.
- Set up the API Gateway WebSocket for the real-time results push flow back to the app — the most challenging architectural piece remaining.
- Assist member A in exactly defining the WebSocket message format that Flutter needs to listen to.