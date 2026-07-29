---
title: "Frontend deployment"
date: 2026-07-29
weight: 4
chapter: false
pre: " <b>5.4.4.</b> "
---

## Read public runtime identifiers

CloudFormation outputs contain public browser configuration identifiers, not passwords or AWS keys. Keep their active values out of this report.

```powershell
$WorkshopRepository = "<path-to-finsight-ai>"
$WorkshopProfile = "finsight-dev"
$WorkshopRegion = "ap-southeast-1"
$WorkshopStack = "finsight-ai-dev"

Set-Location $WorkshopRepository

$WorkshopApiUrl = aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile --query "Stacks[0].Outputs[?OutputKey=='ApiBaseUrl'].OutputValue | [0]" --output text
$WorkshopUserPoolId = aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile --query "Stacks[0].Outputs[?OutputKey=='FrontendUserPoolId'].OutputValue | [0]" --output text
$WorkshopUserPoolClientId = aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile --query "Stacks[0].Outputs[?OutputKey=='FrontendUserPoolClientId'].OutputValue | [0]" --output text
$WorkshopIdentityPoolId = aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile --query "Stacks[0].Outputs[?OutputKey=='FrontendIdentityPoolId'].OutputValue | [0]" --output text
$WorkshopFrontendBucket = aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile --query "Stacks[0].Outputs[?OutputKey=='FrontendBucketName'].OutputValue | [0]" --output text
$WorkshopDistributionId = aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile --query "Stacks[0].Outputs[?OutputKey=='FrontendDistributionId'].OutputValue | [0]" --output text
$WorkshopFrontendUrl = aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile --query "Stacks[0].Outputs[?OutputKey=='FrontendUrl'].OutputValue | [0]" --output text
```

## Generate runtime configuration

```powershell
Set-Location (Join-Path $WorkshopRepository "frontend")
corepack pnpm install --frozen-lockfile
corepack pnpm run build

$RuntimeConfig = @{
  region = $WorkshopRegion
  apiUrl = $WorkshopApiUrl
  userPoolId = $WorkshopUserPoolId
  userPoolClientId = $WorkshopUserPoolClientId
  identityPoolId = $WorkshopIdentityPoolId
  analysisProvider = "GEMINI"
  selfRegistrationEnabled = $true
} | ConvertTo-Json

[System.IO.File]::WriteAllText(
  (Join-Path (Resolve-Path .\dist).Path "config.json"),
  $RuntimeConfig
)
```

The runtime file contains no secret. Never add the Gemini key, temporary credentials, tokens, passwords, or document identifiers.

## Upload to the private frontend bucket

```powershell
aws s3 sync .\dist\ "s3://$WorkshopFrontendBucket" `
  --exclude "index.html" `
  --exclude "config.json" `
  --cache-control "public,max-age=31536000,immutable" `
  --region $WorkshopRegion `
  --profile $WorkshopProfile

aws s3 cp .\dist\index.html "s3://$WorkshopFrontendBucket/index.html" `
  --content-type "text/html" `
  --cache-control "no-cache" `
  --region $WorkshopRegion `
  --profile $WorkshopProfile

aws s3 cp .\dist\config.json "s3://$WorkshopFrontendBucket/config.json" `
  --content-type "application/json" `
  --cache-control "no-store" `
  --region $WorkshopRegion `
  --profile $WorkshopProfile

aws cloudfront create-invalidation `
  --distribution-id $WorkshopDistributionId `
  --paths "/*" `
  --region $WorkshopRegion `
  --profile $WorkshopProfile

Set-Location $WorkshopRepository
```

![CloudFront distribution deployed and invalidation completed](/images/5-Workshop/5.4-Deployment/cloudfront-deployed.png)

Open the value stored in **$WorkshopFrontendUrl**. The page should show FinSight AI with account creation and sign-in controls. Direct public access to the S3 origin must remain blocked.

![FinSight AI sign-in page served through CloudFront](/images/5-Workshop/5.4-Deployment/frontend-landing-page.png)
