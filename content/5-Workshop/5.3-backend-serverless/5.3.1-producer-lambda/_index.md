---
title: "5.3.1 Producer Lambda"
date: 2026-07-07
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---

## Role

Receives the REST request from the client (with a JWT already verified by the Cognito Authorizer), packages it into a message, pushes it to the SQS Main Queue, and returns `202 Accepted` immediately — without waiting for the Worker to finish processing.

## Main code (`src/producer/index.mjs`)

```javascript
export const handler = async (event) => {
  const userId = event.requestContext.authorizer.claims.sub;
  const body = JSON.parse(event.body || "{}");
  const { connectionId, action = "check-gmail" } = body;

  const message = {
    jobId: `job-${Date.now()}-${Math.random().toString(36).slice(2, 8)}`,
    userId, connectionId, action,
    requestedAt: new Date().toISOString()
  };

  await sqs.send(new SendMessageCommand({
    QueueUrl: QUEUE_URL,
    MessageBody: JSON.stringify(message)
  }));

  return {
    statusCode: 202,
    body: JSON.stringify({ message: "Processing started", jobId: message.jobId })
  };
};
```

`userId` is read directly from `event.requestContext.authorizer.claims.sub` — API Gateway already verifies the JWT through the Cognito Authorizer before this Lambda is invoked, so there's no need to verify the token manually in code.

## SAM Template — exposing it as a REST endpoint

```yaml
ProducerFunction:
  Type: AWS::Serverless::Function
  Properties:
    FunctionName: inboxiq-producer
    CodeUri: src/producer/
    Handler: index.handler
    Timeout: 10
    Role: !Ref LambdaRoleArn
    Environment:
      Variables:
        SQS_QUEUE_URL: !Ref MainQueueUrl
    Events:
      CheckGmail:
        Type: Api
        Properties:
          RestApiId: !Ref RestApi
          Path: /check-gmail
          Method: POST
```

> **Fixed from code review:** The first draft had 2 duplicate resources (`ProducerFunction` with no Events + a separate `CheckGmailApiEvent` that actually received the request) — merged into the single resource above to avoid dead code in the template.

## Deployment result

REST API endpoint: `https://rjc76njhya.execute-api.us-east-1.amazonaws.com/prod`

Tested with `curl.exe` using a real JWT token (obtained via `aws cognito-idp initiate-auth`), returning the expected `202 Accepted`:

```json
{"message":"Processing started","jobId":"job-1783438359558-mq2qy4"}
```

![Producer test succeeded](/images/5-Workshop/5.3-backend-serverless/producer-test-202.jpg)
