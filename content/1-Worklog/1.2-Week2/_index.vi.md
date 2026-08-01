---
title: "Nhật ký Tuần 2 - Anh Đức"
date: 2026-06-29
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

**Thời gian:** 29/06/2026 – 05/07/2026

## Mục tiêu Tuần 2

- Hiểu cơ chế presigned upload của Amazon S3.
- Nắm access pattern của DynamoDB cho danh sách và chi tiết tài liệu.
- Thiết kế trải nghiệm upload, theo dõi và xóa tài liệu.
- Chuẩn bị test case cho các ranh giới upload.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| Đầu tuần | Tìm hiểu S3 presigned POST và policy conditions. | Thiết kế client nhận upload contract rồi gửi PDF trực tiếp tới S3 mà không nhận AWS secret. |
| Đầu tuần | Học S3 Block Public Access, versioning và mã hóa. | Xác định thông tin an toàn cần hiển thị, không tạo liên kết public tới PDF. |
| Giữa tuần | Tìm hiểu DynamoDB Query, partition key và pagination. | Thiết kế danh sách tài liệu phân trang theo owner và trạng thái. |
| Giữa tuần | Học cách AWS SDK xử lý request và lỗi dịch vụ. | Xây dựng các trạng thái chọn file, đang tải, xác nhận và lỗi an toàn. |
| Cuối tuần | Nghiên cứu kiểm thử trust boundary. | Tạo test case cho PDF thật, file giả, file quá lớn, key bị sửa và xóa lặp lại. |

## Kết quả đạt được trong Tuần 2

- Hoàn thiện thiết kế trải nghiệm upload, danh sách, chi tiết và xóa tài liệu.
- Phân biệt rõ lỗi client, lỗi upload S3 và lỗi xác nhận backend.
- Kiểm chứng frontend không giữ access key dài hạn hoặc URL tài liệu public.
- Chuẩn bị bộ test bao phủ các điều kiện upload quan trọng.
