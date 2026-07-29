---
title: "Week 2 Worklog"
date: 2026-06-29
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

**Period:** 29 Jun 2026 – 05 Jul 2026

## Week 2 Objectives

- Learn private and versioned Amazon S3 storage.
- Build a secure browser-to-S3 PDF upload flow.
- Design DynamoDB document metadata and lifecycle states.
- Implement owner-scoped document APIs.
- Apply idempotency and safe deletion.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| Early week | I studied S3 Block Public Access, encryption, versioning, object ownership, and lifecycle considerations. | FinSight AI stored PDFs in a private, encrypted, versioned bucket with no public object access. |
| Early week | I learned how constrained presigned POST policies limit file size, MIME type, object key, and encryption headers. | The upload flow allowed direct PDF transfer to S3 while keeping the backend in control of every trusted upload field. |
| Midweek | I studied file validation using the `%PDF-` signature, declared size, metadata, and SHA-256 integrity. | Lambda confirmation verified the uploaded object before moving the document into a trusted state. |
| Midweek | I learned DynamoDB partition and sort keys, conditional updates, and explicit lifecycle states. | Document metadata was stored separately from PDF contents and partitioned by authenticated owner. |
| Late week | I studied API Gateway and Lambda request validation, idempotency, pagination, and version-aware deletion. | The project implemented owner-scoped list, detail, and delete APIs with safe repeated requests and structured error responses. |

## Week 2 Achievements

- Implemented secure PDF upload without making the S3 bucket or objects public.
- Stored document metadata separately from PDF contents in DynamoDB.
- Completed owner-scoped list, detail, pagination, and delete operations.
- Prevented cross-user document access by deriving ownership from authenticated request context.
- Added idempotent creation, confirmation, and deletion behavior for safe retries.
- Verified upload and document-management behavior with local and AWS integration tests.
- Learned that upload security requires coordinated controls across API Gateway, Lambda, IAM, DynamoDB, and S3.
