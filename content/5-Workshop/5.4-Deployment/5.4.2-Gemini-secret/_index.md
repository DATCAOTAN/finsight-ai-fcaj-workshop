---
title: "Gemini secret"
date: 2026-07-29
weight: 2
chapter: false
pre: " <b>5.4.2.</b> "
---

Use the AWS Secrets Manager console in **ap-southeast-1**:

1. Open **Secrets Manager** and choose **Store a new secret**.
2. Choose **Other type of secret**.
3. Store one JSON key named **GEMINI_API_KEY** and paste the provider key as its value.
4. Name the secret **finsight-ai/dev/gemini-api-key**.
5. Do not enable automatic rotation for this short-lived workshop secret.
6. Create the secret, open its detail page, and copy only its ARN.

![Gemini secret created in AWS Secrets Manager](/images/5-Workshop/5.4-Deployment/gemini-secret-created.png)

The stored value has this shape, but the workshop must never contain the real value:

```json
{
  "GEMINI_API_KEY": "<provider-key-entered-only-in-secrets-manager>"
}
```

Verify only the secret metadata from PowerShell:

```powershell
$WorkshopProfile = "finsight-dev"
$WorkshopRegion = "ap-southeast-1"
$WorkshopGeminiSecretId = "finsight-ai/dev/gemini-api-key"

aws secretsmanager describe-secret `
  --secret-id $WorkshopGeminiSecretId `
  --region $WorkshopRegion `
  --profile $WorkshopProfile `
  --query "{Name:Name,ARN:ARN,DeletedDate:DeletedDate}" `
  --output table
```

Do not run **get-secret-value** for screenshots or evidence. Set a local variable containing the ARN, not the key:

```powershell
$WorkshopGeminiSecretArn = aws secretsmanager describe-secret `
  --secret-id $WorkshopGeminiSecretId `
  --region $WorkshopRegion `
  --profile $WorkshopProfile `
  --query "ARN" `
  --output text

$WorkshopGeminiSecretArn
```

The SAM template passes only this ARN to the analysis Lambda. Its IAM role receives Secrets Manager read permission for that exact ARN; the key is loaded at runtime and is never a CloudFormation parameter or frontend value.
