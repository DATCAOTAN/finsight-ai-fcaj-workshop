---
title: "Week 7 Worklog"
date: 2026-08-03
publishDate: 2026-07-29
weight: 7
---

**Period:** 3–9 August 2026

## Week 7 Objectives

- Complete self-service registration and email-confirmation flows.
- Make document failures understandable, recoverable, and safe to retry.
- Activate Gemini through the existing provider boundary for development validation.
- Define and enforce the data-egress boundary for external analysis.
- Validate both a successful long-document path and an oversized-input rejection path.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| 3 August | I studied the Cognito registration and email-confirmation lifecycle. | Added Cognito self-registration, email confirmation, resend, and sign-in guidance while keeping unconfirmed accounts blocked. |
| 4 August | I learned how authentication feedback can remain useful without exposing sensitive account details. | Mapped common registration and confirmation failures to safe, understandable messages. |
| 5 August | I studied failure classification, retry cooldowns, and attempt limits for controlled recovery. | Classified processing failures and allowed only eligible failed documents to re-enter the workflow. |
| 6 August | I studied the trust boundary created when an external provider analyzes application data. | Activated Gemini `gemini-2.5-flash` through the provider abstraction and verified that original PDF binaries remain in AWS; only trusted, extracted page text is sent for analysis. |
| 7 August | I learned why input limits must be enforced before a provider request is made. | Enforced the 1,000,000-character analysis limit with explicit rejection instead of silent truncation or automatic fallback. |
| 8–9 August | I studied boundary testing with representative long and oversized documents. | Ran a 214,091-character document through one Gemini request and exercised a 1,368,551-character document that was rejected before any provider request. |

## Week 7 Achievements

- Completed user registration, confirmation, resend, and sign-in transitions with safe handling for unconfirmed accounts.
- Added understandable error messages for expected authentication and registration conditions.
- Introduced controlled recovery for eligible document failures with cooldown and maximum-attempt safeguards.
- Activated Gemini `gemini-2.5-flash` as the development analysis provider without changing the explicit provider-selection model or adding automatic fallback.
- Kept original PDF binaries inside AWS and limited external transmission to trusted extracted page text, making the hybrid AWS-and-Gemini boundary clear.
- Successfully processed a 214,091-character document to `ANALYZED` with exactly one Gemini provider request.
- Rejected a 1,368,551-character document as `ANALYSIS_INPUT_TOO_LARGE` with zero provider requests, confirming that oversized input is neither truncated nor sent externally.
