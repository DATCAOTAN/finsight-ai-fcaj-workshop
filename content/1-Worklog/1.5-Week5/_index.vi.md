---
title: "Tuần 5"
date: 2026-07-20
weight: 5
pre: " <b> 1.5. </b> "
---

**Thời gian:** 20–26/07/2026

## Mục tiêu Tuần 5

- Triển khai Cognito User Pool và Identity Pool.
- Bảo vệ API Gateway bằng AWS_IAM/SigV4.
- Thực thi ownership từ identity đã xác minh.
- Phân phối frontend qua CloudFront với S3 origin private.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| 20/07 | Học User Pool, app client, token và email confirmation. | Khai báo User Pool không có client secret trong trình duyệt. |
| 21/07 | Tìm hiểu Identity Pool và authenticated role. | Đổi token lấy temporary credentials và tắt unauthenticated identity. |
| 22/07 | Nghiên cứu API Gateway AWS_IAM và SigV4. | Chỉ cho phép request được ký bằng role Cognito hợp lệ. |
| 23–24/07 | Học cách lấy identity từ request context. | Suy ra owner phía server; không tin owner ID do client gửi. |
| 25–26/07 | Tìm hiểu CloudFront OAC và private S3 origin. | Triển khai frontend HTTPS mà không public frontend bucket. |

## Kết quả đạt được trong Tuần 5

- Người dùng đã xác thực nhận temporary credentials và gọi API bằng SigV4.
- Request không ký trả 403; foreign-owner operation trả 404 an toàn.
- Ownership isolation được kiểm tra bằng hai principal.
- Frontend được phục vụ qua CloudFront với S3 origin private.
