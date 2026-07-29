---
title: "Điều kiện tiên quyết"
date: 2026-07-29
weight: 2
chapter: false
pre: " <b>5.2.</b> "
---

## Công cụ cục bộ

Cài đặt và kiểm tra:

- Git;
- Python 3.12;
- Node.js 20.19 trở lên;
- pnpm 11;
- AWS CLI v2;
- AWS SAM CLI;
- editor và PowerShell.

```powershell
git --version
py -3.12 --version
node --version
corepack --version
aws --version
sam --version
```

## Môi trường AWS

Sử dụng tài khoản development hoặc sandbox riêng. Cấu hình AWS CLI profile và xác nhận profile trỏ đúng account, đúng Region trước khi tạo tài nguyên:

```powershell
$WorkshopProfile = "finsight-dev"
$WorkshopRegion = "ap-southeast-1"

aws configure --profile $WorkshopProfile
aws configure get region --profile $WorkshopProfile
aws sts get-caller-identity `
  --profile $WorkshopProfile `
  --region $WorkshopRegion
```

Region dự kiến là **ap-southeast-1**. Dừng lại nếu caller hoặc Region không đúng môi trường workshop.

## Quyền triển khai

Người triển khai cần quyền tạo và cập nhật các tài nguyên được khai báo trong SAM template: CloudFormation, IAM role, Lambda và Layer, API Gateway, S3, DynamoDB, SQS, Step Functions, CloudWatch và Logs, Cognito, CloudFront cùng tham chiếu Secrets Manager.

Deployment dùng **CAPABILITY_NAMED_IAM** vì CloudFormation tạo các execution role có tên và quyền tối thiểu. Hãy yêu cầu quản trị viên cấp role triển khai tạm thời, giới hạn trong FinSight stack dành riêng cho workshop.

## Gemini và tài liệu đầu vào

- Tạo hoặc chuẩn bị Gemini API key cho một development project có kiểm soát.
- Không lưu key vào source control hoặc SAM parameter.
- Chuẩn bị một PDF có văn bản nhúng, nhỏ hơn 10 MiB và không chứa dữ liệu riêng tư, khách hàng, credential, y tế hoặc dữ liệu được quản lý.
- PDF scan chỉ có hình ảnh không phù hợp với luồng thành công vì hệ thống chưa triển khai OCR.

## Repository

Clone repository [DATCAOTAN/finsight-ai](https://github.com/DATCAOTAN/finsight-ai) và chuyển vào thư mục gốc:

```powershell
git clone https://github.com/DATCAOTAN/finsight-ai.git
Set-Location .\finsight-ai
corepack pnpm --version
git status --short --branch
```

Bắt đầu từ revision sạch đã được review. Các lệnh phía sau giả định thư mục gốc có **infrastructure**, **backend**, **frontend**, **scripts** và **samconfig.toml**.
