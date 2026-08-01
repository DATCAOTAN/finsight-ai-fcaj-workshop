---
title: "Weeks 7–8 Worklog"
date: 2026-08-03
publishDate: 2026-07-29
weight: 7
pre: " <b> 1.7. </b> "
---

**Period:** 3–15 August 2026

## Objectives

- Complete registration, analysis, and failure recovery.
- Verify end-to-end security, operations, and quality.
- Finalise AWS First Cloud Journey documentation and handover readiness.

## Tấn Đạt

### AWS knowledge

| Topic | Knowledge gained |
|---|---|
| Cognito and IAM | Reinforced self-registration, email confirmation, temporary credentials, and owner isolation. |
| Serverless reliability | Learned bounded retry, idempotency, DLQ recovery, and safe provider-error classification. |
| AWS operations | Learned CloudFormation lifecycle, CloudWatch alarm recovery, cost evidence, and destructive cleanup. |

### Planned work

- Activated Gemini for development through Secrets Manager while retaining Bedrock as source/template default and disabling automatic fallback.
- Enforced a trusted input limit without silent truncation and classified input, payload, rate-limit, unavailable, and unknown failures.
- Verified stack, IAM, private S3, two principals, queue/DLQ, alarms, logs, and secrets; cleaned only temporary test resources when appropriate.

## Anh Đức

### AWS knowledge

| Topic | Knowledge gained |
|---|---|
| Cognito self-registration | Learned sign-up, confirmation codes, resend-code flow, and safe authentication errors. |
| CloudFront release verification | Learned invalidation, production-asset checks, and verification of the currently served build. |
| AWS evidence and cost | Learned to collect CloudFormation, CloudWatch, S3, and Cognito evidence and report only available cost data. |

### Planned work

- Completed self-registration, email confirmation, resend-code flow, and real-email browser acceptance.
- Built Vietnamese analysis-failure UX with retry cooldown, duplicate-submit prevention, and logical document-splitting guidance.
- Finalised the bilingual Hugo workshop, architecture diagram, evidence images, demo guide, and handover checklist.

## Planned results and evidence

- Registration, email confirmation, sign-in, upload, extraction, analysis, and result retrieval operate end to end.
- Oversized input is rejected before provider invocation; transient failures use bounded retry and size failures are never retried.
- Cross-owner access, unsigned requests, private S3, queues/DLQ, and CloudWatch alarms are verified.
- Backend, frontend, SAM/CloudFormation, and Hugo documentation checks pass the final gate.
- Architecture, Worklog, and workshop guidance match the deployed runtime; destructive cleanup remains deferred until after the demo.
