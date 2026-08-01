---
title: "Nhật ký Tuần 5 - Anh Đức"
date: 2026-07-20
weight: 5
pre: " <b> 1.5. </b> "
---

**Thời gian:** 20–26/07/2026

## Mục tiêu Tuần 5

- Hiểu luồng xác thực Cognito User Pool và Identity Pool.
- Ký request API bằng temporary credentials và SigV4.
- Xây dựng React/Vite SPA cho các luồng tài liệu chính.
- Kiểm tra bản production được phân phối qua CloudFront.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| 20/07 | Tìm hiểu User Pool token, app client và vòng đời phiên. | Tích hợp đăng nhập, đăng xuất và xử lý tài khoản chưa xác nhận. |
| 21/07 | Học Identity Pool đổi token lấy temporary AWS credentials. | Lấy phiên AWS ngắn hạn mà không lưu access key dài hạn trong trình duyệt. |
| 22/07 | Nghiên cứu AWS Signature Version 4. | Ký request list, upload, detail, result và delete tới API Gateway. |
| 23–24/07 | Học mẫu giao diện cho tác vụ bất đồng bộ. | Xây dựng SPA với trạng thái loading, empty, processing, completed và failed. |
| 25–26/07 | Tìm hiểu CloudFront OAC, cache và SPA fallback. | Kiểm tra production build qua HTTPS với S3 origin riêng tư. |

## Kết quả đạt được trong Tuần 5

- Hoàn thành giao diện đăng nhập và quản lý tài liệu cốt lõi.
- Request API từ trình duyệt được ký SigV4 bằng credential ngắn hạn.
- Frontend không chứa client secret hoặc khóa AWS dài hạn.
- Browser acceptance xác nhận luồng đăng nhập, upload và xem trạng thái hoạt động.
