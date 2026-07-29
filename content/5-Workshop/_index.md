---
title: "Workshop"
date: 2026-07-29
weight: 5
chapter: false
pre: " <b>5.</b> "
---

FinSight AI is a serverless AWS application that securely uploads financial PDFs, extracts embedded text by page, and produces a structured analysis with citations. This workshop deploys the verified development architecture in **ap-southeast-1** and uses **Google Gemini gemini-2.5-flash** as the explicitly selected analysis provider.

{{% notice warning %}}
Use an isolated development AWS account and a non-sensitive PDF. Never publish AWS account IDs, active endpoints, Cognito identifiers, document keys, credentials, tokens, API keys, or real financial records.
{{% /notice %}}

[![FinSight AI end-to-end workshop flow](/images/5-Workshop/5.1-Overview/workshop-end-to-end-flow.svg)](/images/5-Workshop/5.1-Overview/workshop-end-to-end-flow.svg)

*Figure: The complete FinSight AI workshop path from local validation to cleanup. Select the image to view it at full size.*

## Learning outcomes

After completing the workshop, you will be able to:

- validate the FinSight AI source locally;
- store a Gemini API key in AWS Secrets Manager without placing it in source control;
- deploy the backend and AWS infrastructure with AWS SAM;
- build and publish the private CloudFront-hosted frontend;
- register a confirmed Cognito user and analyze a PDF end to end;
- verify owner isolation, private storage, asynchronous processing, monitoring, and cleanup.

## Workshop content

1. [Overview](5.1-overview/)
2. [Prerequisites](5.2-prerequisites/)
3. [Architecture](5.3-architecture/)
4. [Deployment](5.4-deployment/)
5. [End-to-end demo](5.5-demo/)
6. [Security and operational verification](5.6-verification/)
7. [Cleanup](5.7-cleanup/)

The workshop uses placeholders such as **&lt;profile&gt;**, **&lt;exact-secret-arn&gt;**, and **&lt;path-to-pdf&gt;**. Replace them only in your local terminal. Do not commit their active values.
