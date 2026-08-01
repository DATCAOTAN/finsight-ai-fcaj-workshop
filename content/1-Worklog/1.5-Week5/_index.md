---
title: "Week 5 Worklog - Tan Dat"
date: 2026-07-20
weight: 5
pre: " <b> 1.5. </b> "
---

**Period:** 20–26 July 2026

## Week 5 Objectives

- Deploy Cognito User Pool and Identity Pool.
- Protect API Gateway with AWS_IAM/SigV4.
- Enforce ownership from verified identity.
- Deliver the frontend through CloudFront and a private S3 origin.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| 20 Jul | Learned User Pools, app clients, tokens, and email confirmation. | Declared a User Pool without a browser client secret. |
| 21 Jul | Studied Identity Pools and authenticated roles. | Exchanged tokens for temporary credentials and disabled unauthenticated access. |
| 22 Jul | Learned API Gateway `AWS_IAM` and SigV4. | Required requests signed by the valid Cognito role. |
| 23–24 Jul | Studied identity in request context. | Derived owner server-side instead of trusting a client owner ID. |
| 25–26 Jul | Learned CloudFront OAC and private origins. | Served the frontend over HTTPS without a public bucket. |

## Week 5 Achievements

- Authenticated users obtained temporary credentials and signed API requests.
- Unsigned requests returned `403`; foreign-owner operations returned safe `404`.
- Verified ownership isolation with two principals.
- Delivered the frontend through CloudFront with a private S3 origin.
