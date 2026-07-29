---
title: "Prerequisites"
date: 2026-07-29
weight: 2
chapter: false
pre: " <b>5.2.</b> "
---

## Local tools

Install and verify:

- Git;
- Python 3.12;
- Node.js 20.19 or newer;
- pnpm 11;
- AWS CLI v2;
- AWS SAM CLI;
- an editor and PowerShell.

```powershell
git --version
py -3.12 --version
node --version
corepack --version
aws --version
sam --version
```

## AWS environment

Use a dedicated development account or sandbox. Configure an AWS CLI profile and confirm that it resolves to the intended account and region before creating anything:

```powershell
$WorkshopProfile = "finsight-dev"
$WorkshopRegion = "ap-southeast-1"

aws configure --profile $WorkshopProfile
aws configure get region --profile $WorkshopProfile
aws sts get-caller-identity `
  --profile $WorkshopProfile `
  --region $WorkshopRegion
```

The expected region is **ap-southeast-1**. Stop if the caller or region is not the intended workshop environment.

## Deployment permissions

The deployer must be allowed to create and update the resources declared by the SAM template: CloudFormation, IAM roles, Lambda and Layers, API Gateway, S3, DynamoDB, SQS, Step Functions, CloudWatch and Logs, Cognito, CloudFront, and Secrets Manager references.

The deployment uses **CAPABILITY_NAMED_IAM** because CloudFormation creates named least-privilege execution roles. Ask the account administrator for a temporary workshop deployment role that is restricted to the dedicated FinSight stack. Do not copy the broad EC2, VPC, Route 53, and wildcard policy from the original sample workshop; FinSight does not require those services.

## Gemini and input document

- Create or obtain a Gemini API key for a controlled development project.
- Do not paste the key into Markdown, source files, SAM parameters, shell history, screenshots, or chat.
- Prepare one text-based PDF under 10 MiB with no private, customer, credential, medical, or regulated data.
- A scanned image-only PDF is unsuitable for the success path because OCR is not implemented.

## Repository

Clone [DATCAOTAN/finsight-ai](https://github.com/DATCAOTAN/finsight-ai) and enter its root directory:

```powershell
git clone https://github.com/DATCAOTAN/finsight-ai.git
Set-Location .\finsight-ai
corepack pnpm --version
git status --short --branch
```

Start from a clean, reviewed revision. The commands in later sections assume the repository root contains **infrastructure**, **backend**, **frontend**, **scripts**, and **samconfig.toml**.
