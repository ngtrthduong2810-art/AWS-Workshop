---
title: "Overview"
date: 2026-07-07
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

## Project Introduction

**InboxIQ** is an AI assistant that summarizes and categorizes emails, helping users (students, office workers) who receive 50–100 emails/day and lack the time to read them all. The system automatically summarizes content, categorizes priority levels, and suggests actions for each email.

- **Client:** Flutter (mobile app)
- **Architecture:** Serverless, Event-Driven on AWS
- **AI Provider:** OpenAI API (GPT-4o-mini)
- **AWS Region:** us-east-1

> **Why use OpenAI instead of Amazon Bedrock?** AWS Free Tier accounts are not granted access to Bedrock. The system is designed following **AI Provider Abstraction** — separating the AI calling layer from the business logic — allowing for a future switch to Bedrock without modifying the overall architecture.

## Overall Architecture (5 layers)

![InboxIQ Architecture](/images/5-Workshop/5.1-overview/architecture-en.png)

| Layer | Component |
|---|---|
| **1. User** | Users, Web/Mobile App (Flutter) |
| **2. Backend** | Cognito, API Gateway (REST + WebSocket), Lambda (Producer + Worker + ws-whoami) |
| **3. Workflow** | SQS (Main Queue + Dead-Letter Queue), EventBridge Scheduler (optional) |
| **4. Storage** | DynamoDB (6 tables), Secrets Manager, Systems Manager Parameter Store |
| **5. Monitoring** | CloudWatch, X-Ray, IAM Role |
| **External** | Gmail API, OpenAI API (outside AWS Cloud) |

## Processing Flow (13 steps)

| # | From → To | Description |
|---|---|---|
| setup | App → API Gateway WebSocket | Connect with JWT → Lambda Authorizer verifies → app calls the `whoami` route to receive a `connectionId` (the `$connect` route cannot reliably push messages back to the client, so a dedicated route is required) |
| 1 | Users → App | Open app, tap "Check Gmail" |
| 2 | App → Cognito | Authenticate, receive JWT |
| 3 | App → API Gateway REST | Call API with JWT + `connectionId` |
| 4 | API Gateway REST → Lambda Producer | Verify JWT, invoke Producer |
| 5 | Lambda Producer → SQS Main Queue | Package message (along with connectionId), return `202 Accepted` immediately |
| 6 | SQS Main Queue → Lambda Worker | Trigger asynchronous processing (Partial Batch Response) |
| 7a | Lambda Worker → Secrets Manager | Retrieve OpenAI API key (cache at global scope) |
| 7b | Lambda Worker → DynamoDB | Query Gmail OAuth token by UserID |
| 8 | Lambda Worker → Gmail API | Fetch list of unread emails |
| 9 | Lambda Worker → OpenAI API | Summarize + prioritize; emails are processed **in parallel** using `Promise.allSettled` (fail-fast timeout, one failed email doesn't drop the entire batch) |
| 10 | Lambda Worker → DynamoDB | Write summary (EmailSummaries table, TTL 30 days) |
| 11 | Lambda Worker → WebSocket → App | Push results real-time using connectionId |
| 12 | SQS Main → SQS DLQ | When retries > 3 times |
| 13 | EventBridge Scheduler → SQS Main Queue | Trigger automatically every 30 minutes (optional) — push to SQS, do not trigger Worker directly |

> **Note:** The initial Gmail connection flow (OAuth via browser → Lambda callback → deep link `inboxiq://gmail-connected`, including a fallback link since Chrome blocks auto-redirects to custom schemes) is a separate flow, detailed in section 5.4.

## Database Tables (6 DynamoDB tables)

| Table | Partition Key | Sort Key | TTL | Purpose |
|---|---|---|---|---|
| `inboxiq-users` | `userId` | — | ❌ | Basic user information |
| `inboxiq-user-settings` | `userId` | — | ❌ | Personalization settings |
| `inboxiq-gmail-connections` | `userId` | — | ❌ | Gmail OAuth token |
| `inboxiq-email-summaries` | `userId` | `emailId` | ✅ 30 days | Email summaries |
| `inboxiq-processing-jobs` | `jobId` | — | ✅ 7 days | Processing status (backup for debugging, not used in MVP) |
| `inboxiq-ws-connections` | `connectionId` | — | ✅ 2 hours | Mapping connectionId ↔ userId |

## Estimated Costs (Free Tier + OpenAI)

| Cost Source | /month at demo scale |
|---|---|
| AWS (Cognito, API GW, Lambda, SQS, DynamoDB, SSM, CloudWatch, X-Ray, EventBridge) | ~$0 (within free tier) |
| WebSocket connection-minute | ~$0.10 |
| OpenAI GPT-4o-mini | ~$0.30–1.00 |
| **Total** | **~$0.50–1.50/month** |

## Known Limitations

1. No multi-region failover yet — acceptable for the MVP, noted as a future development direction.
2. No CI/CD pipeline yet — manual deployment using SAM CLI is sufficient for reporting purposes.
3. Rate limiting currently relies on global API Gateway throttling, lacking a per-user usage plan.
4. Lambda runtime Node.js 20.x has passed EOL (04/2026) — held off on upgrading mid-project to mitigate risk, expected to upgrade to Node.js 22 in a later phase.
5. WebSockets can silently drop when the app is in the background — currently, the app reads the latest `connectionId` and manually reconnects when "Check Gmail" is tapped; there is no active auto-reconnect mechanism when the app resumes (`WidgetsBindingObserver`), which is a planned improvement.