---
title: "Security and verification"
date: 2026-07-29
weight: 6
chapter: false
pre: " <b>5.6.</b> "
---

Run these checks after the demo. They are read-only.

## Stack and private buckets

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

Both buckets must block public access. The documents bucket must report server-side encryption.

![S3 buckets used by the workshop](/images/5-Workshop/5.6-Verification/s3-block-public-access.png)

## Queue, workflow, and alarms

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

After processing settles, the queue and DLQ should be empty, no execution should remain running, and the alarm query should return no active workshop alarm.

![A successful Step Functions execution](/images/5-Workshop/5.6-Verification/step-functions-succeeded.png)

![Workshop CloudWatch alarms are in OK state](/images/5-Workshop/5.6-Verification/cloudwatch-alarms-ok.png)
