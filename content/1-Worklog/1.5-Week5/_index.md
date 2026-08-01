---
title: "Week 5 Worklog - Anh Duc"
date: 2026-07-20
weight: 5
pre: " <b> 1.5. </b> "
---

**Period:** 20–26 July 2026

## Week 5 Objectives

- Understand Cognito User Pool and Identity Pool authentication.
- Sign API requests with temporary credentials and SigV4.
- Build the React/Vite SPA for core document flows.
- Verify the production build delivered through CloudFront.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| 20 Jul | Studied User Pool tokens, app clients, and session lifecycle. | Integrated sign-in, sign-out, and unconfirmed-account handling. |
| 21 Jul | Learned Identity Pool token exchange. | Obtained short-lived AWS credentials without storing long-lived keys. |
| 22 Jul | Studied AWS Signature Version 4. | Signed list, upload, detail, result, and delete API requests. |
| 23–24 Jul | Learned UI patterns for asynchronous work. | Built loading, empty, processing, completed, and failed states. |
| 25–26 Jul | Studied CloudFront OAC, caching, and SPA fallback. | Verified the production build over HTTPS with a private S3 origin. |

## Week 5 Achievements

- Completed sign-in and core document-management views.
- Signed browser API requests with short-lived credentials.
- Kept client secrets and long-lived AWS keys out of the frontend.
- Passed browser acceptance for sign-in, upload, and document status.
