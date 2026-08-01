---
title: "Nhật ký Tuần 5"
date: 2026-07-20
weight: 5
pre: " <b> 1.5. </b> "
---

**Thời gian:** 20–26/07/2026

## Mục tiêu

- Thêm xác thực người dùng bằng Amazon Cognito.
- Cho trình duyệt gọi API được bảo vệ bằng AWS_IAM/SigV4.
- Phân phối frontend qua CloudFront với S3 origin riêng tư.

## Tấn Đạt

### Kiến thức AWS

| Nội dung | Kiến thức đạt được |
|---|---|
| Cognito User Pool | Hiểu authentication, token, app client và xác nhận email. |
| Cognito Identity Pool | Hiểu đổi token lấy temporary AWS credentials và tắt unauthenticated identity. |
| CloudFront và S3 OAC | Hiểu phân phối HTTPS từ origin riêng tư, cache và Origin Access Control. |

### Công việc thực hiện

- Khai báo User Pool, Identity Pool, authenticated role và policy gọi API trong SAM.
- Cấu hình API Gateway dùng `AWS_IAM`; backend suy ra owner từ identity đã xác minh.
- Triển khai frontend bucket riêng tư, CloudFront distribution và OAC.

## Anh Đức

### Kiến thức AWS

| Nội dung | Kiến thức đạt được |
|---|---|
| Cognito authentication flow | Hiểu sign-in, token lifecycle, sign-out và xử lý tài khoản chưa xác nhận. |
| SigV4 trong trình duyệt | Hiểu ký request bằng temporary credentials và tự làm mới phiên hợp lệ. |
| CloudFront deployment | Hiểu cache invalidation, SPA fallback và cấu hình runtime cho bản production. |

### Công việc thực hiện

- Xây dựng React/Vite SPA cho đăng nhập, upload, danh sách, chi tiết, trạng thái và kết quả.
- Tích hợp Cognito và ký SigV4 mà không lưu access key dài hạn trong trình duyệt.
- Viết unit test và chạy browser acceptance cho đăng nhập, upload và ownership-safe responses.

## Kết quả và bằng chứng

- Người dùng đăng nhập nhận temporary credentials và gọi API bằng SigV4.
- Request không ký trả `403`; người dùng khác truy cập tài liệu nhận `404` an toàn.
- Frontend được phục vụ qua HTTPS mà frontend bucket không public.
