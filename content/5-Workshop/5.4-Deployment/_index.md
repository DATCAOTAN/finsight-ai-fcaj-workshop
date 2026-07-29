---
title: "Deployment"
date: 2026-07-29
weight: 4
chapter: false
pre: " <b>5.4.</b> "
---

[![FinSight AI deployment sequence](/images/5-Workshop/5.4-Deployment/deployment-sequence.svg)](/images/5-Workshop/5.4-Deployment/deployment-sequence.svg)

*Figure: The two-pass SAM and frontend deployment sequence.*

Deployment has four stages:

1. [Validate the source locally](5.4.1-local-validation/)
2. [Store the Gemini key safely](5.4.2-gemini-secret/)
3. [Deploy the AWS backend](5.4.3-backend/)
4. [Build and publish the frontend](5.4.4-frontend/)

The first SAM deployment uses the local frontend origin so CloudFormation can create the distribution. After CloudFront returns its HTTPS URL, deploy the same stack a second time with that exact origin. This ensures API Gateway and S3 CORS accept the deployed browser.
