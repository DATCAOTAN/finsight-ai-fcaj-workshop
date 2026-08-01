---
title: "Week 2 Worklog - Anh Duc"
date: 2026-06-29
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

**Period:** 29 June–5 July 2026

## Week 2 Objectives

- Understand Amazon S3 presigned uploads.
- Learn DynamoDB access patterns for document list and detail views.
- Design document upload, status, and deletion interactions.
- Prepare upload-boundary test cases.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| Early week | Studied S3 presigned POST and policy conditions. | Designed a client that posts the backend contract directly to S3 without receiving AWS secrets. |
| Early week | Learned S3 Block Public Access, versioning, and encryption. | Exposed only safe metadata and no public PDF link. |
| Midweek | Studied DynamoDB Query, partition keys, and pagination. | Designed an owner-scoped, paginated document list. |
| Midweek | Learned AWS SDK request and service-error handling. | Built selecting, uploading, confirming, and safe-error states. |
| Late week | Studied trust-boundary testing. | Added cases for valid, fake, oversized, key-tampered, and repeatedly deleted files. |

## Week 2 Achievements

- Completed upload, list, detail, and delete interaction design.
- Distinguished client, S3 upload, and backend confirmation failures.
- Verified that the frontend stores no long-lived key or public document URL.
- Prepared tests for the important upload boundaries.
