---
title: "Triển khai frontend"
date: 2026-07-29
weight: 4
chapter: false
pre: " <b>5.4.4.</b> "
---

## Đọc public runtime identifier

CloudFormation output chứa các browser configuration identifier công khai mà frontend cần sử dụng.

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

## Sinh runtime configuration

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

Runtime file không chứa secret. Không thêm Gemini key, credential tạm thời, token, password hoặc document identifier.

## Upload vào frontend bucket riêng tư

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

![CloudFront distribution đã triển khai và invalidation đã hoàn tất](/images/5-Workshop/5.4-Deployment/cloudfront-deployed.png)

Mở giá trị trong **$WorkshopFrontendUrl**. Trang phải hiển thị FinSight AI cùng chức năng tạo tài khoản và đăng nhập. Truy cập công khai trực tiếp vào S3 origin vẫn phải bị chặn.

![Trang đăng nhập FinSight AI được phục vụ qua CloudFront](/images/5-Workshop/5.4-Deployment/frontend-landing-page.png)
