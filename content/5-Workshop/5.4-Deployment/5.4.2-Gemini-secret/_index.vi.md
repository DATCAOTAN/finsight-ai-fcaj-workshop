---
title: "Gemini secret"
date: 2026-07-29
weight: 2
chapter: false
pre: " <b>5.4.2.</b> "
---

Sử dụng AWS Secrets Manager console tại **ap-southeast-1**:

1. Mở **Secrets Manager** và chọn **Store a new secret**.
2. Chọn **Other type of secret**.
3. Lưu một JSON key có tên **GEMINI_API_KEY** và dán provider key làm value.
4. Đặt tên secret là **finsight-ai/dev/gemini-api-key**.
5. Không bật rotation tự động cho secret workshop tồn tại ngắn hạn này.
6. Tạo secret, mở trang chi tiết và chỉ sao chép ARN.

![Gemini secret đã được tạo trong AWS Secrets Manager](/images/5-Workshop/5.4-Deployment/gemini-secret-created.png)

Giá trị lưu có cấu trúc sau nhưng workshop tuyệt đối không chứa giá trị thật:

```json
{
  "GEMINI_API_KEY": "<provider-key-entered-only-in-secrets-manager>"
}
```

Chỉ kiểm tra metadata của secret từ PowerShell:

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

Không chạy **get-secret-value**. Tạo biến cục bộ chứa ARN, không chứa key:

```powershell
$WorkshopGeminiSecretArn = aws secretsmanager describe-secret `
  --secret-id $WorkshopGeminiSecretId `
  --region $WorkshopRegion `
  --profile $WorkshopProfile `
  --query "ARN" `
  --output text

$WorkshopGeminiSecretArn
```

SAM template chỉ truyền ARN này cho analysis Lambda. IAM role của Lambda chỉ được đọc secret theo chính xác ARN đó; key được tải lúc runtime và không bao giờ là CloudFormation parameter hoặc frontend value.
