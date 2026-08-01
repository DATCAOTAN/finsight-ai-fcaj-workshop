---
title: "Nhật ký Tuần 3"
date: 2026-07-06
weight: 3
pre: " <b> 1.3. </b> "
---

**Thời gian:** 06–12/07/2026

## Mục tiêu

- Xây dựng nền tảng xử lý tài liệu bất đồng bộ, có retry và DLQ.
- Khởi chạy workflow theo cách idempotent.
- Trích xuất văn bản nhúng theo từng trang PDF.

## Tấn Đạt

### Kiến thức AWS

| Nội dung | Kiến thức đạt được |
|---|---|
| DynamoDB Streams | Hiểu stream record, event source mapping và cách phát hiện chuyển trạng thái tài liệu. |
| Amazon SQS và DLQ | Hiểu at-least-once delivery, visibility timeout, retry và redrive policy. |
| AWS Step Functions | Hiểu Standard Workflow, execution name xác định và giới hạn dữ liệu state. |

### Công việc thực hiện

- Kết nối `DynamoDB Streams → dispatcher Lambda → SQS → consumer Lambda → Step Functions`.
- Bổ sung điều kiện trạng thái và execution name xác định để sự kiện trùng không tạo workflow sai.
- Thiết lập queue mã hóa, DLQ, visibility timeout và quyền IAM theo đúng tài nguyên.

## Kết quả và bằng chứng

- Tài liệu `UPLOADED` được đưa vào hàng đợi và khởi chạy một workflow hợp lệ.
- Duplicate message không tạo xử lý trùng; lỗi lặp lại được redrive vào DLQ.
- Workflow chỉ truyền metadata; PDF và artifact vẫn nằm trong S3 riêng tư.
