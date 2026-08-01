---
title: "Week 3"
date: 2026-07-06
weight: 3
pre: " <b> 1.3. </b> "
---

**Period:** 6–12 July 2026

## Week 3 Objectives

- Understand SQS, DLQ, and Step Functions processing visibility.
- Extract embedded text page by page.
- Measure extraction quality and identify requires_ocr.
- Keep large artifacts in S3 instead of DynamoDB or workflow state.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| 06 Jul | Learned SQS visibility, in-flight messages, and DLQs. | Defined UI states for queued and failed documents. |
| 07 Jul | Learned to inspect Step Functions execution history. | Traced documents through validation, extraction, and failure paths. |
| 08 Jul | Studied embedded-text extraction and scanned-PDF limits. | Implemented page-aware extraction with preserved page numbers. |
| 09–10 Jul | Learned the S3 artifact pattern and item/state limits. | Stored extraction JSON in S3 and metadata only in DynamoDB. |
| 11–12 Jul | Studied extraction quality gates. | Calculated non-empty pages, characters, coverage, and requires_ocr. |

## Week 3 Achievements

- Preserved correct page numbers for embedded-text PDFs.
- Created a private S3 extraction artifact.
- Marked insufficient text instead of producing an invalid result.
- Completed tests for valid, empty, malformed, encrypted, and image-only PDFs.
