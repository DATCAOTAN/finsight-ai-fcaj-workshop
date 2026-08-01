---
title: "Weeks 7–8"
date: 2026-08-03
publishDate: 2026-07-29
weight: 7
pre: " <b> 1.7. </b> "
---

**Period:** 3–15 August 2026

## Weeks 7–8 Objectives

- Complete Cognito self-registration and email confirmation.
- Provide clear, safe, actionable analysis-failure UX.
- Verify that CloudFront serves the intended production build.
- Finalise the workshop, diagrams, evidence, and demo guide.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| 03–04 Aug | Studied Cognito sign-up, confirmation, and resend-code flows. | Completed registration, email confirmation, and safe invalid-code handling. |
| 05–06 Aug | Learned transient and non-retryable failure classification. | Presented input, payload, rate-limit, unavailable, and unknown errors in Vietnamese. |
| 07–09 Aug | Studied retry cooldown and duplicate-submit prevention. | Disabled retry during active requests and preserved documents for retry or deletion. |
| 10–12 Aug | Learned CloudFront invalidation and release verification. | Checked production assets, existing sessions, and new-user registration on the live site. |
| 13–15 Aug | Learned FCAJ architecture and evidence presentation. | Finalised bilingual Hugo content, AWS diagrams, evidence, demo instructions, and Worklog. |

## Planned Weeks 7–8 Outcomes

- Registration, email confirmation, sign-in, and returning-user sign-in are verified in production.
- Failure UX states that upload/extraction succeeded, no complete result exists, and which action is appropriate.
- Long documents receive logical splitting guidance; image compression is not presented as a text-token fix.
- Frontend production, browser acceptance, and Hugo documentation pass the final gate.
- Workshop documentation matches the verified runtime, provider, and system limits.
