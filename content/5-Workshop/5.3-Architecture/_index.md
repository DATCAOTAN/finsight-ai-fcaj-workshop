---
title: "Architecture"
date: 2026-07-29
weight: 3
chapter: false
pre: " <b>5.3.</b> "
---

The browser application is delivered by CloudFront from a private S3 origin. Amazon Cognito confirms the user and exchanges User Pool tokens for temporary Identity Pool credentials. The browser signs every application API request with AWS Signature Version 4.

![FinSight AI runtime architecture](/images/2-Proposal/finsight-ai-architecture.svg?v=3ec0ffd1)

## Request and processing flow

1. API Gateway accepts only AWS_IAM-authorized application routes.
2. The upload Lambda creates an owner-scoped object key and a constrained five-minute presigned POST.
3. The browser uploads the PDF directly to the private versioned documents bucket.
4. Confirmation validates metadata, size, PDF signature, and SHA-256 before marking the document trusted.
5. DynamoDB Streams, encrypted SQS, and an idempotent consumer start one Step Functions Standard workflow.
6. The workflow validates the request, extracts embedded text by page, and invokes the analysis Lambda.
7. Only the analysis Lambda reads the exact Gemini secret and sends trusted extracted text to gemini-2.5-flash.
8. The validated result is stored in private versioned S3; DynamoDB stores bounded metadata and hashes.
9. The owner retrieves the result through the protected Result API.

## Security design

- S3 Block Public Access is enabled for both application buckets.
- CloudFront uses Origin Access Control to read the private frontend bucket.
- The browser has no direct IAM permission to read the documents bucket.
- Separate Lambda roles restrict each function to its required resources.
- The backend derives ownership from trusted API Gateway identity context.
- Missing documents and documents owned by another user return the same safe response.
- Logs and metrics exclude document text, provider payloads, credentials, tokens, and secret values.

## External-provider boundary

Gemini is enabled only when the trusted deployment sets **AnalysisProvider=gemini**, **ExternalAiEgressEnabled=true**, and an exact Secrets Manager ARN. The original PDF, owner identity, AWS identifiers, object keys, and credentials do not leave AWS. There is no silent truncation and no automatic fallback to another provider.
