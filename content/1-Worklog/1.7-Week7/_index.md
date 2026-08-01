---
title: "Weeks 7–8 Worklog - Tan Dat"
date: 2026-08-03
publishDate: 2026-07-29
weight: 7
pre: " <b> 1.7. </b> "
---

**Period:** 3–15 August 2026

## Weeks 7–8 Objectives

- Activate the development provider behind a server-side boundary.
- Classify analysis failures and retry only appropriate causes.
- Verify end-to-end security, stack, queues, alarms, and logs.
- Complete operational evidence and cleanup planning.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| 03–04 Aug | Studied provider egress and Secrets Manager runtime access. | Activated Gemini development, retained Bedrock default, and disabled automatic fallback. |
| 05–06 Aug | Learned local input, provider payload, and rate-limit distinctions. | Mapped stable categories without inferring PDF length from HTTP status alone. |
| 07–09 Aug | Studied bounded retry and idempotent recovery. | Retried transient failures only; never retried oversized payloads or silently truncated input. |
| 10–12 Aug | Learned CloudFormation lifecycle and AWS security verification. | Checked stack, IAM, private S3, unsigned requests, and cross-owner access. |
| 13–15 Aug | Studied queue/alarm health, cost evidence, and cleanup. | Verified queue/DLQ and alarms, reported only real cost data, and deferred destructive cleanup until after demo. |

## Planned Weeks 7–8 Outcomes

- Upload, extraction, analysis, and result retrieval operate end to end with server-selected development provider.
- Oversized input is rejected before provider invocation without truncation or inappropriate retry.
- Stack, IAM, S3, ownership, queues/DLQ, CloudWatch, and secret scans pass the final gate.
- Bedrock remains source/template default while live acceptance remains account-quota blocked.
- The main stack remains deployed for demo; destructive cleanup occurs only when the environment is finished.
