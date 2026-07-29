---
title: "Cleanup"
date: 2026-07-29
weight: 7
chapter: false
pre: " <b>5.7.</b> "
---

Cleanup có hai mức. Sử dụng routine cleanup khi development stack dùng chung cần được giữ lại. Chỉ xóa toàn stack khi môi trường workshop chuyên dụng không còn cần thiết.

## Routine demo cleanup

1. Xóa mọi PDF workshop bằng **Delete document** trên frontend.
2. Xác nhận list theo owner đã trống.
3. Đăng xuất.
4. Tra cứu chính xác Cognito username tạm trước khi xóa:

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

Không purge SQS, tự xóa DynamoDB row hoặc làm trống bucket dùng chung.

## Xóa toàn stack

{{% notice warning %}}
Đây là thao tác phá hủy. Chỉ tiếp tục sau khi xác nhận **finsight-ai-dev** và cả hai bucket name chỉ thuộc workshop này. Hãy lưu bằng chứng đã loại bỏ dữ liệu nhạy cảm trước.
{{% /notice %}}

Kiểm tra chính xác target:

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

Làm trống frontend bucket riêng tư. Sau đó dùng helper trong repository cho
documents bucket chuyên dụng có versioning; helper yêu cầu nhập đầy đủ bucket
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

Xác nhận stack đã bị xóa:

```powershell
aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile
```

Kết quả mong đợi là stack-not-found. Cuối cùng, lên lịch xóa có khả năng recovery cho Gemini secret chuyên dụng:

```powershell
aws secretsmanager delete-secret `
  --secret-id $WorkshopGeminiSecretId `
  --recovery-window-in-days 7 `
  --region $WorkshopRegion `
  --profile $WorkshopProfile
```

![Gemini secret đã được lên lịch xóa](/images/5-Workshop/5.7-Cleanup/28.%20gemini-secret-pending-deletion.png)

Kiểm tra AWS Billing và dashboard của Gemini provider sau cleanup. Không giả định credit khiến mọi usage miễn phí.
