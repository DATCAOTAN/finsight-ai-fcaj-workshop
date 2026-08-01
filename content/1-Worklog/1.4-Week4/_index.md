---
title: "Week 4 Worklog - Tan Dat"
date: 2026-07-13
weight: 4
pre: " <b> 1.4. </b> "
---

**Period:** 13–19 July 2026

## Week 4 Objectives

- Orchestrate validation and extraction with Step Functions.
- Design retry, catch, and recoverable failures.
- Separate IAM roles by Lambda function.
- Establish CloudWatch logs, metrics, and alarms.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| 13 Jul | Learned Step Functions Task, Retry, Catch, and terminal states. | Modelled validation, extraction, and failure handling. |
| 14 Jul | Studied Lambda execution roles and resource permissions. | Separated roles for API, dispatcher, consumer, and processing tasks. |
| 15 Jul | Learned structured logging and correlation fields. | Logged by document/workflow without content or credentials. |
| 16–17 Jul | Studied CloudWatch EMF and metric filters. | Emitted Lambda, workflow, and extraction failure metrics. |
| 18–19 Jul | Learned alarms and evaluation windows. | Created alarms for errors, queue backlog, DLQ, and workflow failure. |

## Week 4 Achievements

- Added bounded retry and clear workflow failure paths.
- Removed global IAM wildcards and limited each Lambda role.
- Added CloudWatch logs, metrics, and alarms for key failures.
- Verified intentional-test alarms automatically return to `OK`.
