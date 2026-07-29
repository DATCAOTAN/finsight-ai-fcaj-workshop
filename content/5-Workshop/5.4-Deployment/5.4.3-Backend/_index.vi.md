---
title: "Triển khai backend"
date: 2026-07-29
weight: 3
chapter: false
pre: " <b>5.4.3.</b> "
---

## Xác nhận môi trường đích

```powershell
$WorkshopRepository = "<path-to-finsight-ai>"
$WorkshopProfile = "finsight-dev"
$WorkshopRegion = "ap-southeast-1"
$WorkshopStack = "finsight-ai-dev"
$WorkshopGeminiSecretId = "finsight-ai/dev/gemini-api-key"

Set-Location $WorkshopRepository

$WorkshopGeminiSecretArn = aws secretsmanager describe-secret `
  --secret-id $WorkshopGeminiSecretId `
  --region $WorkshopRegion `
  --profile $WorkshopProfile `
  --query "ARN" `
  --output text

aws sts get-caller-identity `
  --region $WorkshopRegion `
  --profile $WorkshopProfile

aws cloudformation describe-stacks `
  --stack-name $WorkshopStack `
  --region $WorkshopRegion `
  --profile $WorkshopProfile
```

Phản hồi stack-not-found là bình thường ở lần triển khai đầu. Nếu stack đã tồn tại, phải review trước khi cập nhật.

## Khai báo bộ parameter development đã review

```powershell
$WorkshopParameters = @(
  "StageName=dev",
  "MaxFileSizeBytes=10485760",
  "MaxExtractionArtifactBytes=12582912",
  "AnalysisProvider=gemini",
  "ExternalAiEgressEnabled=true",
  "GeminiApiKeySecretArn=$WorkshopGeminiSecretArn",
  "GeminiModelId=gemini-2.5-flash",
  "GeminiMaxOutputTokens=8192",
  "AnalysisMaxInputChars=1000000",
  "PresignedUrlExpirySeconds=300",
  "DefaultPageSize=20",
  "MaxPageSize=100",
  "MaxListQueryRounds=5",
  "DeleteClaimTimeoutSeconds=120",
  "LogRetentionDays=7",
  "ProcessingQueueVisibilityTimeoutSeconds=90",
  "ProcessingQueueRetentionSeconds=345600",
  "ProcessingDlqRetentionSeconds=1209600",
  "ProcessingMaxReceiveCount=3",
  "ProcessingConsumerTimeoutSeconds=30",
  "ProcessingQueueAgeAlarmSeconds=300",
  "EnableSelfRegistration=true"
)
```

## Lần triển khai đầu

```powershell
$InitialWorkshopParameters = $WorkshopParameters + "FrontendOrigin=http://localhost:5173"

sam build `
  --template-file infrastructure/template.yaml `
  --config-env dev

sam deploy `
  --config-env dev `
  --stack-name $WorkshopStack `
  --region $WorkshopRegion `
  --profile $WorkshopProfile `
  --capabilities CAPABILITY_NAMED_IAM `
  --resolve-s3 `
  --confirm-changeset `
  --parameter-overrides $InitialWorkshopParameters
```

Review CloudFormation change set. Change set chỉ nên tạo các tài nguyên serverless FinSight AI được mô tả trong kiến trúc. Chỉ xác nhận khi account, Region, stack name và IAM change đều chính xác.

## Đặt origin của frontend đã triển khai

Đọc CloudFront URL vừa tạo:

```powershell
$WorkshopFrontendUrl = aws cloudformation describe-stacks `
  --stack-name $WorkshopStack `
  --region $WorkshopRegion `
  --profile $WorkshopProfile `
  --query "Stacks[0].Outputs[?OutputKey=='FrontendUrl'].OutputValue | [0]" `
  --output text

$WorkshopFrontendUrl
```

Triển khai lại cùng template với chính xác HTTPS origin đó:

```powershell
$DeployedWorkshopParameters = $WorkshopParameters + "FrontendOrigin=$WorkshopFrontendUrl"

sam deploy `
  --config-env dev `
  --stack-name $WorkshopStack `
  --region $WorkshopRegion `
  --profile $WorkshopProfile `
  --capabilities CAPABILITY_NAMED_IAM `
  --resolve-s3 `
  --confirm-changeset `
  --parameter-overrides $DeployedWorkshopParameters
```

Cuối cùng, kiểm tra stack:

```powershell
aws cloudformation describe-stacks `
  --stack-name $WorkshopStack `
  --region $WorkshopRegion `
  --profile $WorkshopProfile `
  --query "Stacks[0].{Status:StackStatus,Outputs:Outputs}" `
  --output json
```

Chỉ tiếp tục khi trạng thái là **CREATE_COMPLETE** hoặc **UPDATE_COMPLETE**. Không công khai các output value được trả về.

![Triển khai CloudFormation stack đã hoàn tất](/images/5-Workshop/5.4-Deployment/cloudformation-stack-complete.png)

![Các tài nguyên FinSight AI do CloudFormation tạo](/images/5-Workshop/5.4-Deployment/cloudformation-resources-summary.png)
