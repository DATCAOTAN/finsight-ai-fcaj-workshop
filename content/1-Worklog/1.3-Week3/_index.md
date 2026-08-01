---
title: "Week 3 Worklog"
date: 2026-07-06
weight: 3
pre: " <b> 1.3. </b> "
---

**Period:** 6–12 July 2026

## Objectives

- Build asynchronous document processing with retries and a DLQ.
- Start workflows idempotently.
- Extract embedded PDF text page by page.

## Tấn Đạt

### AWS knowledge

| Topic | Knowledge gained |
|---|---|
| DynamoDB Streams | Learned stream records, event source mappings, and lifecycle-transition detection. |
| Amazon SQS and DLQ | Learned at-least-once delivery, visibility timeout, retry, and redrive policy. |
| AWS Step Functions | Learned Standard Workflows, deterministic execution names, and state-size limits. |

### Work completed

- Connected `DynamoDB Streams → dispatcher Lambda → SQS → consumer Lambda → Step Functions`.
- Added lifecycle guards and deterministic execution names so duplicate events cannot create invalid workflows.
- Configured encrypted queues, a DLQ, visibility timeout, and resource-scoped IAM permissions.

## Anh Đức

### AWS knowledge

| Topic | Knowledge gained |
|---|---|
| SQS operations | Learned visible/in-flight message states, queue depth, and failed-message observation. |
| Step Functions execution | Learned execution history and how to trace each document-processing step. |
| S3 artifact pattern | Learned per-document artifact prefixes and why large content stays outside workflow state and DynamoDB. |

### Work completed

- Implemented page-aware embedded-text extraction with page numbers and quality statistics.
- Created the extraction JSON artifact in S3 and stored only metadata and `requires_ocr` in DynamoDB.
- Prepared PDF fixtures and tests for text, empty, malformed, encrypted, and image-only documents.

## Results and evidence

- An `UPLOADED` document is queued and starts one valid workflow.
- Duplicate messages do not duplicate processing; repeatedly failing messages are sent to the DLQ.
- The workflow carries metadata only; PDFs and artifacts remain in private S3.
