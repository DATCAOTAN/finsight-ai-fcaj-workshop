---
title: "Week 3 Worklog - Tan Dat"
date: 2026-07-06
weight: 3
pre: " <b> 1.3. </b> "
---

**Period:** 6–12 July 2026

## Week 3 Objectives

- Build event-driven asynchronous processing from DynamoDB changes.
- Configure SQS, DLQ, and an idempotent consumer.
- Start Step Functions with deterministic execution names.
- Keep workflow payloads small and artifacts in S3.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| 06 Jul | Studied DynamoDB Streams and event source mappings. | Detected `PENDING_UPLOAD → UPLOADED` transitions for processing. |
| 07 Jul | Learned SQS at-least-once delivery and visibility timeout. | Configured the processing queue around consumer runtime. |
| 08 Jul | Studied retry and redrive policy. | Sent repeatedly failing messages to a DLQ. |
| 09–10 Jul | Learned idempotent consumers and conditional state. | Prevented duplicate messages from starting duplicate workflows. |
| 11–12 Jul | Studied Step Functions Standard Workflows. | Used deterministic execution names and metadata-only state. |

## Week 3 Achievements

- Completed `DynamoDB Streams → dispatcher → SQS → consumer → Step Functions`.
- Encrypted the queue/DLQ and configured visibility and redrive correctly.
- Prevented duplicate events from creating invalid workflows or artifacts.
- Scoped dispatcher and consumer IAM permissions to required resources.
