---
title: "Week 6 Worklog"
date: 2026-07-27
weight: 6
pre: " <b> 1.6. </b> "
---

**Period:** 27 July–2 August 2026

## Objectives

- Produce schema-valid financial analysis with page citations.
- Protect provider credentials and store provenance.
- Complete owner-scoped result retrieval.

## Tấn Đạt

### AWS knowledge

| Topic | Knowledge gained |
|---|---|
| AWS Secrets Manager | Learned secret ARNs, IAM access, rotation boundaries, and secret-safe logging and templates. |
| Amazon Bedrock | Learned model invocation, account quotas, and its source/template-default role in the system. |
| S3 and DynamoDB | Learned to separate result artifacts from metadata to avoid item limits and reduce data exposure. |

### Work completed

- Built the Analysis Lambda with server-side provider selection; the browser cannot select a model.
- Validated JSON schema, required fields, and page citations before accepting a result.
- Stored result artifacts in private S3 and only safe status, artifact reference, and provenance in DynamoDB.

## Anh Đức

### AWS knowledge

| Topic | Knowledge gained |
|---|---|
| Bedrock model access | Learned the distinction between model configuration, IAM permission, and live account quota. |
| Secrets Manager boundary | Learned that only Lambda reads the secret; the frontend receives no provider key or provider choice. |
| CloudWatch provenance | Learned to record provider/model/version safely without exposing prompts or document data. |

### Work completed

- Built result views for summary, metrics, risks, opportunities, citations, and provenance.
- Presented processing/failed/completed states consistently and never treated partial output as complete.
- Added frontend tests for result schema, page citations, safe messages, and documents without results.

## Results and evidence

- Invalid schema or citations are rejected and never presented as completed analysis.
- The result API uses the owner-scoped compound key and returns no prompt, secret, S3 key, or internal exception.
- Bedrock remains the source/template default; live acceptance is quota-blocked and no automatic provider fallback exists.
