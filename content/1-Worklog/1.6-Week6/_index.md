---
title: "Week 6 Worklog - Anh Duc"
date: 2026-07-27
weight: 6
pre: " <b> 1.6. </b> "
---

**Period:** 27 July–2 August 2026

## Week 6 Objectives

- Understand Bedrock, external-provider, and Secrets Manager boundaries.
- Present structured results with page citations.
- Never display partial output or raw provider errors as complete analysis.
- Verify provenance and safe user messages.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| 27 Jul | Studied Bedrock model access, IAM, and account quota. | Documented Bedrock as source/template default with live acceptance quota-blocked. |
| 28 Jul | Learned the Secrets Manager trust boundary. | Verified that only Analysis Lambda reads the secret and the frontend receives no provider key. |
| 29 Jul | Studied JSON schema and page-citation validation. | Rendered validated schema fields instead of free-form provider responses. |
| 30–31 Jul | Learned safe provenance recording. | Displayed provider, model, and citations without prompts, S3 keys, or exceptions. |
| 01–02 Aug | Studied asynchronous result states. | Distinguished processing, failed, and completed without presenting partial results. |

## Week 6 Achievements

- Completed summary, metrics, risks, opportunities, and citation views.
- Displayed only results that passed schema and citation validation.
- Prevented browser-side provider or model selection.
- Completed tests for valid results, safe failures, and unavailable results.
