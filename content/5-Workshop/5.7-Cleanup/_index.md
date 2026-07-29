---
title: "Cleanup"
date: 2026-07-29
weight: 7
chapter: false
pre: " <b>5.7.</b> "
---

Cleanup has two levels. Use routine cleanup when the shared development stack must remain. Use full-stack deletion only when the dedicated workshop environment is no longer needed.

## Routine demo cleanup

1. Delete every workshop PDF through **Delete document** in the frontend.
2. Confirm the owner-scoped list is empty.
3. Sign out.
4. Look up the exact temporary Cognito username before deleting it:

```powershell
$WorkshopProfile = "finsight-dev"
$WorkshopRegion = "ap-southeast-1"
$WorkshopStack = "finsight-ai-dev"
$WorkshopEmail = "<controlled-workshop-email>"

$WorkshopUserPoolId = aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile --query "Stacks[0].Outputs[?OutputKey=='FrontendUserPoolId'].OutputValue | [0]" --output text

aws cognito-idp admin-get-user `
  --user-pool-id $WorkshopUserPoolId `
  --username $WorkshopEmail `
  --region $WorkshopRegion `
  --profile $WorkshopProfile

aws cognito-idp admin-delete-user `
  --user-pool-id $WorkshopUserPoolId `
  --username $WorkshopEmail `
  --region $WorkshopRegion `
  --profile $WorkshopProfile
```

Do not purge SQS, delete DynamoDB rows manually, or empty shared buckets.

## Full-stack deletion

{{% notice warning %}}
This is destructive. Continue only after confirming that **finsight-ai-dev** and both bucket names belong exclusively to this workshop. Retain sanitized evidence first.
{{% /notice %}}

Inspect exact targets:

```powershell
$WorkshopRepository = "<path-to-finsight-ai>"
$WorkshopProfile = "finsight-dev"
$WorkshopRegion = "ap-southeast-1"
$WorkshopStack = "finsight-ai-dev"
$WorkshopGeminiSecretId = "finsight-ai/dev/gemini-api-key"

Set-Location $WorkshopRepository

$WorkshopFrontendBucket = aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile --query "Stacks[0].Outputs[?OutputKey=='FrontendBucketName'].OutputValue | [0]" --output text
$WorkshopDocumentsBucket = aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile --query "Stacks[0].Outputs[?OutputKey=='DocumentsBucketName'].OutputValue | [0]" --output text

aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile
aws s3api list-objects-v2 --bucket $WorkshopFrontendBucket --region $WorkshopRegion --profile $WorkshopProfile
aws s3api list-object-versions --bucket $WorkshopDocumentsBucket --region $WorkshopRegion --profile $WorkshopProfile
```

Empty the private frontend bucket. Then use the repository helper for the
dedicated versioned documents bucket; it requires typing the complete bucket
name:

```powershell
aws s3 rm "s3://$WorkshopFrontendBucket" `
  --recursive `
  --region $WorkshopRegion `
  --profile $WorkshopProfile

python scripts/empty_versioned_bucket.py `
  --bucket $WorkshopDocumentsBucket `
  --profile $WorkshopProfile `
  --region $WorkshopRegion

sam delete `
  --stack-name $WorkshopStack `
  --region $WorkshopRegion `
  --profile $WorkshopProfile
```

Verify that the stack is gone:

```powershell
aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile
```

The expected response is stack-not-found. Finally, schedule recovery-safe deletion of the dedicated Gemini secret:

```powershell
aws secretsmanager delete-secret `
  --secret-id $WorkshopGeminiSecretId `
  --recovery-window-in-days 7 `
  --region $WorkshopRegion `
  --profile $WorkshopProfile
```

![Gemini secret scheduled for deletion](/images/5-Workshop/5.7-Cleanup/28.%20gemini-secret-pending-deletion.png)

Review AWS Billing and the Gemini provider dashboard after cleanup. Do not assume that credits make usage free.
