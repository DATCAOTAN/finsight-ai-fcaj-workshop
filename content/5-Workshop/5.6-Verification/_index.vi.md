---
title: "Bảo mật và kiểm tra"
date: 2026-07-29
weight: 6
chapter: false
pre: " <b>5.6.</b> "
---

Chạy các kiểm tra chỉ đọc sau khi demo.

## Stack và bucket riêng tư

```powershell
$WorkshopProfile = "finsight-dev"
$WorkshopRegion = "ap-southeast-1"
$WorkshopStack = "finsight-ai-dev"

$WorkshopDocumentsBucket = aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile --query "Stacks[0].Outputs[?OutputKey=='DocumentsBucketName'].OutputValue | [0]" --output text
$WorkshopFrontendBucket = aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile --query "Stacks[0].Outputs[?OutputKey=='FrontendBucketName'].OutputValue | [0]" --output text

aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile --query "Stacks[0].StackStatus" --output text
aws s3api get-public-access-block --bucket $WorkshopDocumentsBucket --region $WorkshopRegion --profile $WorkshopProfile
aws s3api get-public-access-block --bucket $WorkshopFrontendBucket --region $WorkshopRegion --profile $WorkshopProfile
aws s3api get-bucket-encryption --bucket $WorkshopDocumentsBucket --region $WorkshopRegion --profile $WorkshopProfile
```

Cả hai bucket phải block public access. Documents bucket phải báo server-side encryption.

![Các S3 bucket được workshop sử dụng](/images/5-Workshop/5.6-Verification/s3-block-public-access.png)

## Queue, workflow và alarm

```powershell
$WorkshopProfile = "finsight-dev"
$WorkshopRegion = "ap-southeast-1"
$WorkshopStack = "finsight-ai-dev"

$WorkshopQueueUrl = aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile --query "Stacks[0].Outputs[?OutputKey=='ProcessingQueueUrl'].OutputValue | [0]" --output text
$WorkshopDlqUrl = aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile --query "Stacks[0].Outputs[?OutputKey=='ProcessingDeadLetterQueueUrl'].OutputValue | [0]" --output text
$WorkshopStateMachineArn = aws cloudformation describe-stacks --stack-name $WorkshopStack --region $WorkshopRegion --profile $WorkshopProfile --query "Stacks[0].Outputs[?OutputKey=='ProcessingStateMachineArn'].OutputValue | [0]" --output text

aws sqs get-queue-attributes --queue-url $WorkshopQueueUrl --attribute-names ApproximateNumberOfMessages ApproximateNumberOfMessagesNotVisible ApproximateNumberOfMessagesDelayed --region $WorkshopRegion --profile $WorkshopProfile
aws sqs get-queue-attributes --queue-url $WorkshopDlqUrl --attribute-names ApproximateNumberOfMessages --region $WorkshopRegion --profile $WorkshopProfile
aws stepfunctions list-executions --state-machine-arn $WorkshopStateMachineArn --status-filter RUNNING --region $WorkshopRegion --profile $WorkshopProfile
aws cloudwatch describe-alarms --alarm-name-prefix finsight-ai-dev- --state-value ALARM --region $WorkshopRegion --profile $WorkshopProfile
```

Sau khi xử lý ổn định, queue và DLQ phải trống, không còn execution đang chạy và truy vấn alarm không trả về workshop alarm đang hoạt động.

![Một Step Functions execution thành công](/images/5-Workshop/5.6-Verification/step-functions-succeeded.png)

![Các CloudWatch alarm của workshop ở trạng thái OK](/images/5-Workshop/5.6-Verification/cloudwatch-alarms-ok.png)
