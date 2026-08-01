---
title: "Week 2 Worklog - Tan Dat"
date: 2026-06-29
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

**Period:** 29 June–5 July 2026

## Week 2 Objectives

- Implement secure PDF upload with presigned POST.
- Design document metadata and lifecycle in DynamoDB.
- Build owner-scoped list, get, and delete APIs.
- Make retries and version-aware deletion safe.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| Early week | Learned S3 Block Public Access, SSE-KMS, and versioning. | Created a private, encrypted, versioned bucket with no public objects. |
| Early week | Studied presigned POST policy conditions. | Constrained MIME type, size, object key, and encryption headers. |
| Midweek | Learned DynamoDB keys and conditional writes. | Stored metadata by owner/document ID and guarded lifecycle transitions. |
| Midweek | Studied Query, pagination, and opaque tokens. | Built list without Scan and without exposing `LastEvaluatedKey`. |
| Late week | Learned S3 versions, delete markers, and idempotency. | Removed all versions/markers and safely completed the `DELETED` tombstone on retry. |

## Week 2 Achievements

- Valid PDFs reached `UPLOADED`; fake, oversized, and key-tampered files were rejected.
- Verified S3 privacy, encryption, versioning, and Block Public Access.
- Completed owner-scoped list/get/delete and safe pagination.
- Made deletion recoverable across S3 cleanup and DynamoDB tombstoning.
