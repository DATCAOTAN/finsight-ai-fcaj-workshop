---
title: "FinSight AI Project Proposal"
date: 2026-07-29
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

## Serverless Financial Document Intelligence Platform on AWS

### 1. Executive Summary

FinSight AI helps users review public or synthetic financial reports. An authenticated user uploads a private PDF, the system extracts embedded text by page, and AI returns a structured analysis with financial metrics, trends, risks, anomalies, limitations, and page citations.

AWS provides authentication, frontend delivery, protected APIs, private storage, asynchronous processing, security, and monitoring. Google Gemini gemini-2.5-flash is the active external development provider. Amazon Bedrock remains the source/template default, Groq is implemented but inactive, and there is no automatic provider fallback.

The original PDF remains in private AWS storage. Only trusted extracted text and required metadata are sent to Gemini. Results support human review and are not investment advice.

**Team size:** 2 members

### 2. Problem Statement

#### What is the problem?

Financial reports are often long and contain information across many pages. Manual review takes time, important risks may be overlooked, and summaries without page citations are difficult to verify. PDF extraction and AI analysis can also fail, exceed size limits, or take longer than a normal synchronous request.

#### The solution

FinSight AI provides authenticated private upload, asynchronous processing, embedded-text extraction, structured AI analysis, and page-level citations. Ownership is derived by the server, storage remains private, and invalid or incomplete AI responses are rejected.

#### Benefits

- Reduces the time needed to find important financial information.
- Makes findings easier to verify through page citations.
- Demonstrates a secure AWS serverless and event-driven architecture.
- Provides clear processing states, controlled retry, monitoring, and safe deletion.

### 3. Solution Architecture

FinSight AI uses a serverless AWS architecture for secure financial-document processing. The React/Vite frontend is delivered through CloudFront from a private S3 origin. Confirmed users receive temporary credentials from Cognito and sign protected API requests with SigV4. After a verified private PDF upload, DynamoDB Streams, SQS, Lambda, and Step Functions coordinate embedded-text extraction and structured analysis. Validated results remain private and are returned only to the document owner.

![FinSight AI solution architecture](/images/2-Proposal/finsight-ai-architecture.svg?v=3ec0ffd1)

#### AWS Services Used

- **Amazon CloudFront:** Delivers the React/Vite frontend through HTTPS from a private S3 origin.
- **Amazon Cognito:** Handles confirmed-email authentication and temporary AWS credentials.
- **Amazon API Gateway:** Provides the REST API protected by AWS_IAM.
- **AWS Lambda:** Implements document APIs, event dispatch, extraction, analysis, retry, and deletion.
- **Amazon S3:** Privately stores frontend assets, original PDFs, extraction artifacts, and validated results.
- **Amazon DynamoDB:** Stores owner-scoped metadata and lifecycle state; Streams trigger processing.
- **Amazon SQS:** Buffers processing messages and isolates exhausted failures in a DLQ.
- **AWS Step Functions:** Orchestrates the Standard extraction and analysis workflow.
- **Amazon CloudWatch:** Provides structured logs, embedded metrics, 10 alarms, and execution visibility.
- **AWS Secrets Manager:** Protects the selected external-provider credential.

#### Component Design

- **Web interface:** React/Vite supports registration, sign-in, PDF upload, progress, results, citations, retry, and deletion.
- **Authentication:** Cognito User Pool and Identity Pool issue temporary credentials; the browser signs API requests with SigV4.
- **Document management:** The backend derives ownership, verifies PDF metadata and SHA-256, and stores files in private, versioned S3.
- **Asynchronous processing:** DynamoDB Streams and SQS decouple upload confirmation from an idempotent Step Functions workflow.
- **Text extraction:** Lambda extracts embedded text by page and records quality signals; OCR is detected as required but is not executed.
- **AI analysis:** Trusted deployment configuration selects Gemini gemini-2.5-flash; Bedrock remains the source/template default and Groq remains inactive.
- **Result and security:** Schema and page citations are validated locally, results remain private, and foreign access returns a safe not-found response.
- **Observability:** CloudWatch monitors logs, metrics, alarms, queues, failures, and workflow state without storing full document text in logs.

### 4. Technical Implementation

#### Implementation phases

1. Define the project scope, AWS architecture, IAM controls, cost plan, and AWS SAM foundation.
2. Implement private PDF upload, owner-scoped metadata, document APIs, idempotency, and safe deletion.
3. Add DynamoDB Streams, SQS/DLQ, Step Functions, embedded-text extraction, and quality detection.
4. Add Cognito, browser SigV4, the React frontend, structured AI analysis, citation validation, Gemini integration, monitoring, testing, and release documentation.

#### Technical requirements

- React, Vite, TypeScript, Python 3.12, AWS SAM, and CloudFormation.
- AWS managed serverless services listed in the architecture.
- PDF files with embedded text.
- Public, synthetic, or approved non-sensitive reports for Gemini development processing.

OCR, RAG, vector databases, investment recommendations, automatic trading, production SLA, and legal certification are outside the current scope.

### 5. Timeline and Milestones

- **Week 1 — 22/06–28/06:** project definition, AWS foundation, and architecture.
- **Week 2 — 29/06–05/07:** secure upload and document management.
- **Week 3 — 06/07–12/07:** asynchronous processing and PDF extraction.
- **Week 4 — 13/07–19/07:** workflow, security, monitoring, cost, and cleanup.
- **Week 5 — 20/07–26/07:** Cognito, frontend, provider abstraction, and structured analysis.
- **Week 6 — 27/07–02/08:** Gemini integration, failure recovery, and final application validation.
- **Week 7 — 03/08–09/08:** bilingual report, architecture diagram, screenshots, and review.
- **Week 8 — 10/08–15/08:** workshop validation, demo, privacy review, publication, and submission.

### 6. Budget Estimation

The estimate uses the current architecture in Asia Pacific (Singapore) and a low-volume development workload:

- 2 active users;
- 100 PDF documents per month, approximately 1 MiB each;
- 500 protected API requests;
- fewer than 1,000 Lambda invocations and 300 GB-seconds;
- fewer than 5,000 small DynamoDB operations;
- 100 workflows with fewer than 1,000 Step Functions transitions;
- less than 250 MiB of S3 data and versions;
- less than 1 GiB of logs and CloudFront transfer; and
- 100 Gemini analyses.

Prices were reviewed on 29 July 2026 using the [AWS Pricing Calculator](https://calculator.aws/) and official [Gemini API pricing](https://ai.google.dev/gemini-api/docs/pricing).

#### Estimated monthly infrastructure cost

- **Amazon API Gateway:** USD 0.01 for approximately 500 REST requests.
- **AWS Lambda:** USD 0.01 for fewer than 1,000 requests and 300 GB-seconds.
- **Amazon S3:** USD 0.02 for less than 0.25 GiB, versions, and low request volume.
- **Amazon DynamoDB:** USD 0.01 for fewer than 5,000 on-demand operations.
- **Amazon SQS:** USD 0.01 for fewer than 2,000 queue requests.
- **AWS Step Functions:** USD 0.03 for fewer than 1,000 Standard state transitions before any applicable free tier.
- **Amazon CloudWatch:** USD 2.00 conservative allowance for less than 1 GiB of logs, embedded metrics, and 10 standard alarms.
- **Amazon CloudFront:** USD 0.10 for fewer than 10,000 requests and less than 1 GiB transfer.
- **Amazon Cognito:** USD 0.00 expected for 2 monthly active users under the applicable allowance.
- **AWS Secrets Manager:** USD 0.40 for one active Gemini secret and low API-call volume.
- **AWS CloudFormation:** no additional service charge.

**Estimated AWS subtotal: USD 2.59/month, or USD 31.08/12 months before credits and tax.**

#### External AI cost

The paid-tier planning case uses the verified long-document result of 67,723 input tokens and 609 output tokens per analysis. For 100 analyses with Gemini gemini-2.5-flash:

- input: 6.7723 million tokens × USD 0.30 = USD 2.03;
- output: 0.0609 million tokens × USD 2.50 = USD 0.15; and
- **estimated Gemini total: USD 2.18/month, or USD 26.21/12 months.**

Gemini Free Tier could reduce this amount to USD 0 while eligible, but free quota and pricing are not guaranteed.

#### Total planning estimate

**Estimated combined total: USD 4.77/month, or USD 57.29/12 months.**

The AWS learning program provides USD 200 in promotional credits. Based on this workload, the estimated AWS portion is within that ceiling, but AWS credits do not pay the external Gemini charge. Credit eligibility, expiry, tax, actual usage, and future pricing must be checked separately. No dedicated hardware purchase is planned.

### 7. Risk Assessment

#### Main risks

- Bedrock inference remains blocked by account-level quota.
- Extracted text leaves AWS when Gemini is active.
- AI output may be inaccurate, malformed, incomplete, or incorrectly cited.
- Provider rate limits, outages, and input limits may interrupt analysis.
- Scanned PDFs require OCR, which is not implemented.
- Unauthorized access, secret exposure, duplicate events, workflow failure, unexpected cost, and schedule delay remain possible.

#### Mitigation

FinSight AI uses private storage, confirmed-email authentication, temporary credentials, server-derived ownership, schema and citation validation, a 1,000,000-character server limit, controlled retry, DLQ, CloudWatch alarms, Secrets Manager, privacy-safe logs, and public or synthetic development data. No risk is considered completely eliminated.

### 8. Expected Outcomes

- A secure workflow from user authentication and private PDF upload to structured analysis and safe deletion.
- Financial findings with page citations and provider/model provenance.
- Repeatable serverless infrastructure, monitoring, testing, cost controls, and cleanup.
- A bilingual FCAJ report and workshop for demonstrating the verified development workflow.
- A practical AWS learning reference while keeping human review and current system limitations explicit.
