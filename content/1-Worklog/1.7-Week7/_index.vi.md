---
title: "Nhật ký Tuần 7–8"
date: 2026-08-03
publishDate: 2026-07-29
weight: 7
pre: " <b> 1.7. </b> "
---

**Thời gian:** 03–15/08/2026

## Mục tiêu

- Hoàn thiện đăng ký, phân tích và khả năng phục hồi lỗi.
- Kiểm chứng toàn trình bảo mật, vận hành và chất lượng.
- Hoàn thiện tài liệu AWS First Cloud Journey và chuẩn bị bàn giao.

## Tấn Đạt

### Kiến thức AWS

| Nội dung | Kiến thức đạt được |
|---|---|
| Cognito và IAM | Củng cố self-registration, email confirmation, temporary credentials và owner isolation. |
| Serverless reliability | Hiểu bounded retry, idempotency, DLQ recovery và phân loại lỗi provider an toàn. |
| AWS operations | Hiểu CloudFormation lifecycle, CloudWatch alarm recovery, cost evidence và destructive cleanup. |

### Kế hoạch triển khai

- Kích hoạt Gemini cho development bằng Secrets Manager; giữ Bedrock là source/template default và không tự động fallback.
- Áp dụng giới hạn đầu vào tin cậy, không cắt ngầm; phân loại lỗi input, payload, rate limit, unavailable và unknown.
- Chạy kiểm tra stack, IAM, S3 private, hai principal, queue/DLQ, alarm, log và secret scan; chỉ dọn tài nguyên kiểm thử khi phù hợp.

## Anh Đức

### Kiến thức AWS

| Nội dung | Kiến thức đạt được |
|---|---|
| Cognito self-registration | Hiểu sign-up, confirmation code, resend code và các lỗi xác thực cần thông báo an toàn. |
| CloudFront release verification | Hiểu invalidation, kiểm tra asset production và xác nhận bản đang phục vụ sau triển khai. |
| AWS evidence and cost | Hiểu cách thu thập bằng chứng CloudFormation, CloudWatch, S3, Cognito và ghi chi phí đúng dữ liệu thực. |

### Kế hoạch triển khai

- Hoàn thiện self-registration, email confirmation, resend code và browser acceptance bằng email thật.
- Xây dựng UX lỗi phân tích bằng tiếng Việt, retry cooldown, chống gửi trùng và hướng dẫn chia tài liệu theo phần logic.
- Hoàn thiện Hugo workshop song ngữ, sơ đồ kiến trúc, ảnh bằng chứng, hướng dẫn demo và checklist bàn giao.

## Kết quả dự kiến và bằng chứng

- Luồng đăng ký, xác nhận email, đăng nhập, upload, extraction, analysis và result hoạt động toàn trình.
- Tài liệu vượt giới hạn bị từ chối trước provider; lỗi tạm thời có retry giới hạn và lỗi kích thước không retry.
- Cross-owner matrix, unsigned request, S3 private, queue/DLQ và CloudWatch alarms được kiểm chứng.
- Bộ kiểm thử backend, frontend, SAM/CloudFormation và tài liệu Hugo đều vượt qua final gate.
- Tài liệu kiến trúc, Worklog và hướng dẫn workshop phản ánh đúng runtime được triển khai; cleanup phá hủy được hoãn đến sau demo.
