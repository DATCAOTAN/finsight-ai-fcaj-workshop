---
title: "Kiến trúc"
date: 2026-07-29
weight: 3
chapter: false
pre: " <b>5.3.</b> "
---

CloudFront phân phối ứng dụng trình duyệt từ S3 origin riêng tư. Amazon Cognito xác nhận user và đổi User Pool token thành Identity Pool credential tạm thời. Trình duyệt ký mọi API request của ứng dụng bằng AWS Signature Version 4.

![Kiến trúc runtime FinSight AI](/images/2-Proposal/finsight-ai-architecture.svg?v=3ec0ffd1)

## Luồng request và xử lý

1. API Gateway chỉ chấp nhận application route được cấp quyền AWS_IAM.
2. Upload Lambda tạo object key theo owner và presigned POST có ràng buộc trong năm phút.
3. Trình duyệt tải PDF trực tiếp vào documents bucket riêng tư có versioning.
4. Bước confirm kiểm tra metadata, kích thước, chữ ký PDF và SHA-256 trước khi đánh dấu tài liệu đáng tin cậy.
5. DynamoDB Streams, SQS được mã hóa và consumer idempotent khởi chạy một Step Functions Standard workflow.
6. Workflow kiểm tra request, trích xuất văn bản nhúng theo trang và gọi analysis Lambda.
7. Chỉ analysis Lambda được đọc chính xác Gemini secret và gửi văn bản đã tin cậy tới gemini-2.5-flash.
8. Kết quả đã kiểm tra được lưu trong S3 riêng tư có versioning; DynamoDB chỉ lưu metadata có giới hạn và hash.
9. Owner đọc kết quả qua Result API được bảo vệ.

## Thiết kế bảo mật

- S3 Block Public Access được bật cho cả hai application bucket.
- CloudFront dùng Origin Access Control để đọc frontend bucket riêng tư.
- Trình duyệt không có IAM permission đọc trực tiếp documents bucket.
- Các Lambda role tách biệt chỉ truy cập tài nguyên cần thiết.
- Backend suy ra ownership từ identity context đáng tin cậy của API Gateway.
- Tài liệu không tồn tại và tài liệu thuộc user khác trả cùng một phản hồi an toàn.
- Log và metric không chứa document text, provider payload, credential, token hoặc secret value.

## Ranh giới provider bên ngoài

Gemini chỉ được bật khi deployment đáng tin cậy đặt **AnalysisProvider=gemini**, **ExternalAiEgressEnabled=true** và ARN chính xác của Secrets Manager. PDF gốc, owner identity, AWS identifier, object key và credential không rời AWS. Hệ thống không âm thầm cắt input và không tự động fallback sang provider khác.
