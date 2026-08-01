---
title: "Week 6"
date: 2026-07-27
weight: 6
pre: " <b> 1.6. </b> "
---

**Period:** 27 July–2 August 2026

## Week 6 Objectives

- Build Analysis Lambda and the result API.
- Validate JSON schema and page citations.
- Store private result artifacts and safe provenance.
- Protect provider credentials with Secrets Manager.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| 27 Jul | Studied Bedrock InvokeModel, IAM, and quotas. | Retained Bedrock as source/template default and recorded the live quota block. |
| 28 Jul | Learned Secrets Manager and secret ARN policies. | Granted only Analysis Lambda access to the selected provider key. |
| 29 Jul | Studied JSON schema validation. | Rejected missing or mistyped response fields before persistence. |
| 30–31 Jul | Learned citation validation and provenance. | Checked page ranges and stored safe provider/model/version metadata. |
| 01–02 Aug | Studied S3 result artifacts and DynamoDB metadata. | Stored full results in S3 and status/metadata only in DynamoDB. |

## Week 6 Achievements

- Preserved the analysis schema and citation contract.
- Prevented invalid responses from reaching COMPLETED.
- Made the result API owner-scoped without exposing S3 keys or exceptions.
- Kept secrets out of source, templates, frontend assets, and logs.
