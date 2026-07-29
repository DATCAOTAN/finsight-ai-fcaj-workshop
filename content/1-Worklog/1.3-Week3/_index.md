---
title: "Week 3 Worklog"
date: 2026-07-06
weight: 3
---

**Period:** 6–12 July 2026

## Week 3 Objectives

- Study event-driven processing with Amazon S3, EventBridge, Amazon SQS, and AWS Lambda.
- Understand retry, visibility-timeout, dead-letter queue, and idempotency patterns.
- Learn how embedded PDF text can be extracted and evaluated page by page.
- Build a reliable document-processing lifecycle from upload to extracted text.
- Keep document binaries and processing artifacts private while exposing only safe metadata.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| 6 July | I studied how S3 events can drive state changes without direct service coupling. | Connected confirmed S3 uploads to an EventBridge rule so document processing starts only after a real object transition. |
| 7 July | I studied SQS visibility timeouts, retries, and dead-letter queues for durable asynchronous delivery. | Configured the processing queue to absorb bursts and isolate repeated failures. |
| 8 July | I learned why idempotent consumers are necessary when messages can be delivered more than once. | Added lifecycle checks so duplicate delivery does not restart work for a document that is already processing or complete. |
| 9–10 July | I studied embedded PDF text extraction and the value of retaining page boundaries. | Used `pypdf` to extract embedded text page by page and preserved page numbers for later citations. |
| 11–12 July | I learned how quality gates and private artifacts support safe document processing. | Added checks for empty or unusable text, stored extracted content in private S3 objects, and kept DynamoDB records limited to status and artifact metadata. |

## Week 3 Achievements

- Completed an event-driven path from confirmed upload to queued document processing.
- Added retry-aware SQS processing with a dead-letter queue for messages that repeatedly fail.
- Made the consumer idempotent so duplicate events do not create duplicate work.
- Extracted embedded PDF text with page boundaries intact, preparing the data for traceable analysis.
- Added explicit handling for encrypted, unreadable, image-only, or otherwise unusable PDFs instead of silently producing weak output.
- Kept original PDFs and extracted artifacts private in S3 while returning only safe status information through the application.
- Established clear document states that the API and later user interface could report consistently.
