---
title: "Week 4 Worklog"
date: 2026-07-13
weight: 4
pre: " <b> 1.4. </b> "
---

**Period:** 13–19 July 2026

## Objectives

- Orchestrate stateful and recoverable extraction.
- Narrow IAM permissions for each component.
- Establish operational logs, metrics, and alarms.

## Tấn Đạt

### AWS knowledge

| Topic | Knowledge gained |
|---|---|
| Step Functions | Learned Retry, Catch, failure states, and multi-step workflow recovery. |
| IAM | Learned execution roles, resource-level permissions, and per-Lambda role separation. |
| Amazon CloudWatch | Learned Logs, Embedded Metric Format, metric filters, alarms, and evaluation windows. |

### Work completed

- Modelled validation, extraction, and failure handling in the state machine.
- Separated IAM roles for API, dispatcher, consumer, and processing Lambdas.
- Added structured logs, metrics, and alarms for Lambda errors, workflow failures, queue backlog, and DLQ messages.

## Results and evidence

- The workflow recovers transient errors and records controlled terminal failures.
- IAM has no global wildcard; each Lambda reaches only the resources it needs.
- Alarms respond to intentional failure tests and return to `OK` after the evaluation window clears.
