---
title: "Week 4 Worklog - Anh Duc"
date: 2026-07-13
weight: 4
pre: " <b> 1.4. </b> "
---

**Period:** 13–19 July 2026

## Week 4 Objectives

- Use CloudWatch to inspect logs, metrics, and alarms.
- Build AWS regression tests for completed phases.
- Verify that logs expose no sensitive data.
- Standardise operational and evidence checklists.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| 13 Jul | Studied CloudWatch Logs and Logs Insights. | Queried document/request failures without recording PDF text or credentials. |
| 14 Jul | Learned CloudWatch Metrics, EMF, and alarm evaluation. | Checked alarms for Lambda, workflow, queue backlog, and DLQ. |
| 15 Jul | Learned `OK`, `ALARM`, and `INSUFFICIENT_DATA`. | Confirmed that intentional-test alarms automatically return to `OK`. |
| 16–17 Jul | Learned AWS CLI evidence collection. | Checked stack status, queue attributes, alarm state, and resource policies. |
| 18–19 Jul | Studied negative security testing. | Checked logs for credentials, JWTs, active presigned URLs, and document text. |

## Week 4 Achievements

- Completed regression tests for upload, document management, queues, and extraction.
- Verified correct alarm activation and automatic recovery.
- Found no sensitive data in the reviewed logs.
- Completed the stack, queue/DLQ, alarm, test, and controlled-cleanup checklist.
