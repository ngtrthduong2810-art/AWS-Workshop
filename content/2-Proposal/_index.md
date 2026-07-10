---
title: "Proposal"
date: 2026-07-04
weight: 3
chapter: false
pre: " <b> 2. </b> "
---

# InboxIQ

## AI-powered email triage on Serverless AWS

### 1. Project Overview

InboxIQ is an intelligent virtual assistant that tackles email overload for modern users (students, office workers). The mobile application (Flutter) connects securely to Gmail via the OAuth 2.0 standard, uses an artificial intelligence model (GPT-4o-mini) to summarize content, categorize each email (work / personal / promo / notification) and assess its priority level, then pushes the results back to the app in real time over WebSocket. The entire backend runs on AWS's Serverless Event-Driven architecture (Region `us-east-1`), built within the framework of the First Cloud AI Journey (FCAJ) 2026 internship program.

### 2. Objectives

- Build a complete end-to-end system: from a mobile app running on a real device, through a serverless backend, to external AI/Gmail services — verified with real email data.
- Apply an asynchronous architecture (Producer/Worker via SQS) so the user gets an instant response while heavy processing runs in the background, combined with WebSocket push instead of polling.
- Ensure multi-layered security: user authentication with Cognito (JWT), Gmail read authorization via OAuth 2.0 with minimal scopes, all credentials stored in Secrets Manager, and IAM Roles following the Least Privilege principle.
- Operate the entire project within the AWS Free Tier, with AI spending tightly controlled by a hard limit.
- Manage all infrastructure exclusively through Infrastructure as Code (AWS SAM) and document the full journey — including incidents and lessons learned — as a bilingual Hugo report.

### 3. Problem Statement

Modern users typically receive 50–100 emails per day, spending significant time filtering information and easily missing important messages. Existing solutions are either manual in nature (keyword filters, hand-applied labels) or third-party AI services with high costs and privacy risks, since email data is processed centrally beyond the user's control.

The technical problem breaks down into three core challenges: (1) accessing the user's mailbox safely and with explicit consent (OAuth, never storing the Gmail password); (2) running time-consuming AI processing (several seconds to tens of seconds) without blocking the mobile app; (3) delivering results to the right user, on the right session, in real time.

### 4. Solution Architecture

The system is organized into 5 separated functional layers following the Serverless Event-Driven model:

```
LAYER 1 · USER         → Users, Mobile App (Flutter)
LAYER 2 · BACKEND      → Cognito, API Gateway (REST + WebSocket), Lambda (Producer + Worker + Authorizer)
LAYER 3 · WORKFLOW     → SQS (Main Queue + Dead-Letter Queue), EventBridge Scheduler (optional)
LAYER 4 · STORAGE      → DynamoDB (4 tables, TTL auto-cleanup), Secrets Manager
LAYER 5 · MONITORING   → CloudWatch, X-Ray, IAM Role
EXTERNAL SERVICES      → Gmail API, OpenAI API (outside AWS Cloud)
```

**Main processing flow:** the user taps "Check Gmail" in the app → REST API (JWT-authenticated) → Lambda Producer packages the request together with the `connectionId` into SQS and immediately returns `202 Accepted` → Lambda Worker consumes the message, reads the Gmail token from DynamoDB (auto-refreshing when expired), calls the Gmail API for unread emails, calls GPT-4o-mini to summarize them in parallel → stores the results in DynamoDB (with a 30-day TTL) → pushes the results back to the app through the API Gateway WebSocket.

**AWS services used:**

- **Amazon Cognito**: identity management, user authentication and JWT issuance.
- **Amazon API Gateway**: a REST endpoint for synchronous operations; a WebSocket endpoint (routes `$connect`, `$disconnect`, `whoami`) for the real-time bidirectional channel, authenticated by a Lambda Authorizer.
- **AWS Lambda**: independent compute functions — Authorizer, Producer, Worker, the WebSocket lifecycle handlers and the OAuth flow (init/callback), sharing common logic through a Lambda Layer.
- **Amazon SQS**: the `inboxiq-main` queue (Partial Batch Response — retrying only failed messages) and a Dead-Letter Queue isolating messages that fail after 3 retries, with a CloudWatch Alarm attached.
- **Amazon DynamoDB**: 4 dedicated tables (Gmail connections, email summaries, WebSocket sessions, processing jobs) in On-Demand mode, using TTL for data lifecycle management.
- **AWS Secrets Manager**: secure storage for the OpenAI API key and the Google OAuth Client Secret, read with global-scope caching inside Lambda.
- **Amazon EventBridge Scheduler** (optional): schedules a periodic email check every 30 minutes.
- **CloudWatch & X-Ray**: logs, metrics, alarms and end-to-end tracing.

Since the account within the program has restricted access to Amazon Bedrock, the solution uses the OpenAI API, designed with an AI provider abstraction so it can migrate to Bedrock in the future.

### 5. Timeline

The project is delivered over 3 weeks by a team of 4 members, split into specialized tracks (backend/architecture, Flutter, OAuth/security, documentation/testing/cost):

- **Week 1 — Foundations**: finalize the architecture and work assignments; build the storage tier (DynamoDB, SQS + DLQ) and the identity layer (Cognito, IAM Role, Secrets Manager); write the Lambda Producer/Worker and integrate OpenAI; set up the Google Cloud project and OAuth consent screen; scaffold the Hugo documentation repo and establish cost-monitoring discipline.
- **Week 2 — Core integration**: complete the Gmail OAuth flow (init/callback Lambdas, refresh-token Lambda Layer); build the API Gateway WebSocket with its Authorizer and the `whoami` route; wire real Gmail into the Worker; build the Flutter client side (Cognito authentication, OAuth deep link, WebSocket service); test the pipeline with real email.
- **Week 3 — Final integration and polish**: end-to-end testing on a real Android device, resolving integration incidents; optimize the Worker (parallel processing, per-item fault tolerance); finish the Material 3 UI; run the security review; consolidate documentation, cost figures and the resource-cleanup guide.

### 6. Budget

The infrastructure is designed around the On-Demand model to make full use of the AWS Free Tier:

| Item | Estimated monthly cost | Notes |
| --- | --- | --- |
| AWS Lambda | $0.00 | Within the 1 million requests/month free allowance |
| Amazon SQS & API Gateway | ~$0.00 | MVP request volume is far below Free Tier limits |
| Amazon DynamoDB | $0.00 | On-Demand mode, small data footprint |
| Secrets Manager, CloudWatch, X-Ray | ~$0.00 | Experimental usage; secret caching reduces API calls |
| OpenAI API (GPT-4o-mini) | ~$1.00 – $2.00 | Test volume of 50–100 emails/day; capped at 10 emails per invocation |

Financial risk controls: AWS Budgets email alerts at multiple spending thresholds; a hard limit of **$5.00/month** on the OpenAI Platform; a `maxResults = 10` cap on emails processed per run to prevent cost spikes when the mailbox contains a large backlog of unread emails.

### 7. Risks

**Risk matrix:**

| Risk | Impact | Likelihood |
| --- | --- | --- |
| Gmail OAuth token becomes invalid or lacks scopes (user does not grant full permissions on the consent screen) | High | Medium |
| WebSocket connection drops silently, preventing results from reaching the app | High | Medium |
| Throttling from OpenAI or Secrets Manager under bursts of calls | Medium | Low |
| Uncontrolled AWS/OpenAI cost overruns | High | Low |
| The app only works with accounts on the Test users list (consent screen in Testing mode) | Medium | Certain (known limitation) |

**Mitigation strategies:**

- **Gmail token**: store token state in DynamoDB, validate before each call, auto-refresh through the shared Lambda Layer; check the actual `scope` field in the token response instead of trusting that the consent flow completed successfully.
- **WebSocket**: the client verifies the `connectionId` at the moment of use (never trusting a cached value) and automatically reconnects when the connection is found to be dropped; on the Worker side, the push call is wrapped in its own error handling so a failed push does not fail the whole batch.
- **Throttling**: cache API keys at Lambda's global scope; process emails in parallel with per-item fault tolerance (one failed email does not bring down the whole batch); SQS Partial Batch Response retries only the failed messages.
- **Cost**: AWS Budgets alerts at multiple thresholds; the OpenAI hard limit; the per-run email cap; weekly reviews of the Billing Dashboard.
- **Test users limitation**: accepted as part of the project's scope (Google's verification process for Gmail scopes is beyond the internship's timeframe), documented explicitly in the report's Limitations section together with the procedure for adding test accounts when a demo requires it.
