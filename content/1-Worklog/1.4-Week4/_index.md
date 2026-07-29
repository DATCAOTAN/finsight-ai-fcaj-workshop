---
title: "Week 4 Worklog"
date: 2026-07-13
weight: 4
---

**Period:** 13–19 July 2026

## Week 4 Objectives

- Study AWS Step Functions as a way to make multi-step processing visible and recoverable.
- Understand IAM-authenticated API invocation and least-privilege service roles.
- Learn practical observability with structured logs, metrics, alarms, and health checks.
- Strengthen security boundaries around queues, storage, and workflow execution.
- Prepare repeatable operational checks for deployment and cleanup.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| 13 July | I studied how workflow orchestration makes multi-step processing visible and recoverable. | Modelled extraction, validation, analysis, and completion as explicit Step Functions states with clear success and failure paths. |
| 14 July | I studied IAM-authenticated APIs and AWS Signature Version 4. | Configured the API to use `AWS_IAM` authorization for protected requests. |
| 15 July | I learned how least-privilege boundaries reduce the impact of a compromised component. | Narrowed Lambda, queue, bucket, table, and workflow permissions to the actions and resources each component needs. |
| 16–17 July | I studied structured logs, application metrics, and their role in troubleshooting. | Added structured logs and CloudWatch Embedded Metric Format records for document states, failures, latency, and provider activity. |
| 18–19 July | I learned how alarms, health checks, cost review, and cleanup support operational readiness. | Added CloudWatch alarms and health checks, reviewed queue behaviour and costs, and practised cleanup and secret-scanning checks. |

## Week 4 Achievements

- Replaced an implicit chain of background work with a Step Functions workflow whose progress and failures can be inspected.
- Protected application API calls with IAM authentication and Signature Version 4.
- Reduced broad service permissions by assigning narrowly scoped roles to processing components.
- Added structured operational logs without placing document contents or credentials in log messages.
- Published metrics for document outcomes, processing duration, queue failures, and analysis-provider requests.
- Added CloudWatch alarms covering processing errors, dead-letter queues, workflow failures, and abnormal operating conditions.
- Established repeatable health, cost-awareness, secret-scan, and cleanup checks for later validation.
