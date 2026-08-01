---
title: "Week 2 Worklog"
date: 2026-06-29
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

**Period:** 29 June–5 July 2026

## Objectives

- Build a secure PDF upload path into Amazon S3.
- Design document metadata and lifecycle state in DynamoDB.
- Provide owner-scoped document-management APIs.

## Tấn Đạt

### AWS knowledge

| Topic | Knowledge gained |
|---|---|
| Amazon S3 | Learned Block Public Access, SSE-KMS, versioning, presigned POST, and policy conditions. |
| Amazon DynamoDB | Learned partition and sort keys, conditional updates, Query, and pagination tokens. |
| API Gateway and Lambda | Learned proxy integration, request validation, and per-function IAM roles. |

### Work completed

- Implemented an upload contract that constrains MIME type, size, object key, and encryption.
- Verified PDF signature, size, metadata, and SHA-256 before accepting the document state.
- Built list, get, and delete APIs using the owner/document compound key, including S3 versions and delete markers.

## Results and evidence

- A real PDF moved from `PENDING_UPLOAD` to `UPLOADED`; fake, oversized, and key-tampered files were rejected.
- S3 privacy, encryption, versioning, and Block Public Access were verified.
- Listing uses DynamoDB `Query`; pagination hides `LastEvaluatedKey`, and repeated operations are safe.
