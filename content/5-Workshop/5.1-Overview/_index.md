---
title: "Overview"
date: 2026-07-29
weight: 1
chapter: false
pre: " <b>5.1.</b> "
---

## Scenario

You are deploying a controlled development environment for FinSight AI. A confirmed user signs in through Amazon Cognito, uploads a text-based financial PDF, and receives a structured Gemini analysis without exposing the document bucket or long-lived AWS credentials to the browser.

[![FinSight AI end-to-end workshop flow](/images/5-Workshop/5.1-Overview/workshop-end-to-end-flow.svg)](/images/5-Workshop/5.1-Overview/workshop-end-to-end-flow.svg)

*Figure: Nine controlled stages connect deployment, demonstration, verification, and cleanup. Select the image to view it at full size.*

The workshop follows one complete path:

1. Validate the application locally.
2. Create a dedicated Gemini secret.
3. Deploy the SAM stack.
4. Configure CORS for the generated CloudFront URL.
5. Build and publish the React frontend.
6. Confirm a Cognito account and sign in.
7. Upload, process, inspect, retry if necessary, and delete one non-sensitive PDF.
8. Verify queues, workflow, alarms, and private storage.

## Implemented boundaries

- Maximum upload size is 10 MiB in the development configuration.
- The current extractor reads embedded PDF text; it does not run OCR or Amazon Textract.
- Gemini receives trusted extracted page text and bounded metadata, not the original PDF binary.
- The backend selects the provider. The browser cannot switch providers.
- There is no automatic provider fallback.
- The result is financial-document analysis, not investment advice.

## Time and cost

Allow approximately 90–120 minutes for a first deployment. The stack uses usage-based serverless services and has no continuously running compute. Costs can continue through logs, alarms, S3 versions, CloudFront traffic, and Gemini usage, so complete the cleanup section when the environment is no longer required.
