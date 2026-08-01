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

## Results and evidence

- An `UPLOADED` document is queued and starts one valid workflow.
- Duplicate messages do not duplicate processing; repeatedly failing messages are sent to the DLQ.
- The workflow carries metadata only; PDFs and artifacts remain in private S3.
