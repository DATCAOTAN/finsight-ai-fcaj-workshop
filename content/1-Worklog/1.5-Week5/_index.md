---
title: "Week 5 Worklog"
date: 2026-07-20
weight: 5
---

**Period:** 20–26 July 2026

## Week 5 Objectives

- Study Amazon Cognito user pools and the difference between authentication and authorization.
- Learn how a browser can call an IAM-protected API without embedding long-lived credentials.
- Build the main React journeys for signing in, uploading, and tracking documents.
- Enforce document ownership on the server rather than trusting browser-supplied identity.
- Deliver the frontend through private S3 storage and Amazon CloudFront.

## Learning and implementation activities

| Time | Learning topic | FinSight AI implementation activity |
|---|---|---|
| 20 July | I studied Cognito authentication and the separation between user pools, application clients, and AWS credentials. | Configured a Cognito user pool and application client for authenticated users, with no client secret in the browser and unauthenticated access disabled. |
| 21 July | I learned how a browser can use temporary credentials to sign AWS requests safely. | Used temporary Cognito credentials to sign protected API requests with Signature Version 4. |
| 22 July | I studied the difference between authentication, authorization, and resource ownership. | Derived the user identity from verified request context and applied owner checks to document listing, upload, status, and result operations. |
| 23–24 July | I studied React interaction patterns for asynchronous application journeys. | Built sign-in, document list, upload, status refresh, loading, empty, success, and safe error states. |
| 25–26 July | I learned how CloudFront can deliver a static site while its S3 origin remains private. | Served the React build through CloudFront with a private S3 origin and exercised authentication, ownership, and browser request flows. |

## Week 5 Achievements

- Added Cognito-based sign-in with short-lived AWS credentials for browser sessions.
- Kept long-lived secrets and application-client secrets out of the frontend.
- Signed protected browser requests for the IAM-authorized API.
- Enforced ownership from server-verified identity instead of accepting an owner identifier from the client.
- Completed the core document-management interface, including upload progress and understandable status feedback.
- Added calm loading, empty, and error states so expected failures remain clear to users.
- Published the frontend through CloudFront while keeping the underlying S3 origin private.
