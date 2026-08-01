---
title: "Week 7 Worklog"
date: 2026-08-03
publishDate: 2026-07-29
weight: 7
pre: " <b> 1.7. </b> "
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
| 3 August | Study the Cognito registration and email-confirmation lifecycle. | Add Cognito self-registration, email confirmation, resend, and sign-in guidance while keeping unconfirmed accounts blocked. |
| 4 August | Learn how authentication feedback can remain useful without exposing sensitive account details. | Map common registration and confirmation failures to safe, understandable messages. |
| 5 August | Study failure classification, retry cooldowns, and attempt limits for controlled recovery. | Classify processing failures and allow only eligible failed documents to re-enter the workflow. |
| 6 August | Study the trust boundary created when an external provider analyzes application data. | Activate Gemini gemini-2.5-flash through the provider abstraction and verify that original PDF binaries remain in AWS; send only trusted, extracted page text for analysis. |
| 7 August | Learn why input limits must be enforced before a provider request is made. | Enforce the 1,000,000-character analysis limit with explicit rejection instead of silent truncation or automatic fallback. |
| 8–9 August | Study boundary testing with representative long and oversized documents. | Run a representative long document through one Gemini request and verify that an oversized document is rejected before any provider request. |

## Planned Week 7 Outcomes

- Complete registration, confirmation, resend, and sign-in transitions with safe handling for unconfirmed accounts.
- Add understandable error messages for expected authentication and registration conditions.
- Introduce controlled recovery for eligible document failures with cooldown and maximum-attempt safeguards.
- Activate Gemini gemini-2.5-flash for development without automatic provider fallback.
- Keep original PDF binaries inside AWS and limit external transmission to trusted extracted page text.
- Verify one successful representative long-document analysis.
- Verify that an oversized input is rejected before any provider request.
