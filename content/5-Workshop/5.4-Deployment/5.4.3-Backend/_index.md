---
title: "Backend deployment"
date: 2026-07-29
weight: 3
chapter: false
pre: " <b>5.4.3.</b> "
---

## Confirm the target

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

A stack-not-found response is expected on a first deployment. Any existing stack must be reviewed before it is updated.

## Define the reviewed development parameters

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

## First deployment

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

Review the CloudFormation change set. It should create only the FinSight AI serverless resources described in the architecture. Confirm the change set only after the account, Region, stack name, and IAM changes are correct.

## Set the deployed frontend origin

Read the generated CloudFront URL:

```powershell
$WorkshopFrontendUrl = aws cloudformation describe-stacks `
  --stack-name $WorkshopStack `
  --region $WorkshopRegion `
  --profile $WorkshopProfile `
  --query "Stacks[0].Outputs[?OutputKey=='FrontendUrl'].OutputValue | [0]" `
  --output text

$WorkshopFrontendUrl
```

Deploy the same template again with that exact HTTPS origin:

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

Finally, verify the stack:

```powershell
aws cloudformation describe-stacks `
  --stack-name $WorkshopStack `
  --region $WorkshopRegion `
  --profile $WorkshopProfile `
  --query "Stacks[0].{Status:StackStatus,Outputs:Outputs}" `
  --output json
```

Continue only when the status is **CREATE_COMPLETE** or **UPDATE_COMPLETE**.

![CloudFormation stack deployment completed](/images/5-Workshop/5.4-Deployment/cloudformation-stack-complete.png)

![FinSight AI resources created by CloudFormation](/images/5-Workshop/5.4-Deployment/cloudformation-resources-summary.png)
