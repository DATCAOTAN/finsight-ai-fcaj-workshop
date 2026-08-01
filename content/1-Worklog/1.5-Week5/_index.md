---
title: "Week 5 Worklog"
date: 2026-07-20
weight: 5
pre: " <b> 1.5. </b> "
---

**Period:** 20–26 July 2026

## Objectives

- Add user authentication with Amazon Cognito.
- Let the browser call an AWS_IAM/SigV4-protected API.
- Deliver the frontend through CloudFront with a private S3 origin.

## Tấn Đạt

### AWS knowledge

| Topic | Knowledge gained |
|---|---|
| Cognito User Pool | Learned authentication, tokens, app clients, and email confirmation. |
| Cognito Identity Pool | Learned token exchange for temporary AWS credentials and disabling unauthenticated identities. |
| CloudFront and S3 OAC | Learned HTTPS delivery from a private origin, caching, and Origin Access Control. |

### Work completed

- Declared the User Pool, Identity Pool, authenticated role, and API invocation policy in SAM.
- Configured API Gateway for `AWS_IAM`; the backend derives owner identity from verified context.
- Deployed the private frontend bucket, CloudFront distribution, and OAC.

## Results and evidence

- Signed-in users obtain temporary credentials and call the API with SigV4.
- Unsigned requests return `403`; foreign-owner access returns a safe `404`.
- The frontend is served over HTTPS without making its S3 bucket public.
