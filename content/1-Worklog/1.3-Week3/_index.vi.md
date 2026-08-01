---
title: "Nhật ký Tuần 3 - Tấn Đạt"
date: 2026-07-06
weight: 3
pre: " <b> 1.3. </b> "
---

**Thời gian:** 06–12/07/2026

## Mục tiêu Tuần 3

- Xây dựng nền tảng xử lý bất đồng bộ theo sự kiện DynamoDB.
- Cấu hình SQS, DLQ và consumer idempotent.
- Khởi chạy Step Functions bằng execution name xác định.
- Giữ payload workflow nhỏ và artifact trong S3.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| 06/07 | Tìm hiểu DynamoDB Streams và event source mapping. | Phát hiện chuyển trạng thái `PENDING_UPLOAD → UPLOADED` để tạo sự kiện xử lý. |
| 07/07 | Học SQS at-least-once delivery và visibility timeout. | Cấu hình processing queue phù hợp với thời gian chạy consumer. |
| 08/07 | Nghiên cứu retry và redrive policy. | Thiết lập DLQ cho message thất bại quá số lần nhận cho phép. |
| 09–10/07 | Học idempotent consumer và conditional state. | Ngăn message trùng khởi động nhiều workflow cho cùng tài liệu. |
| 11–12/07 | Tìm hiểu Step Functions Standard Workflow. | Dùng deterministic execution name và chỉ truyền metadata cần thiết. |

## Kết quả đạt được trong Tuần 3

- Hoàn thiện luồng `DynamoDB Streams → dispatcher → SQS → consumer → Step Functions`.
- Queue và DLQ được mã hóa, có visibility timeout và redrive policy phù hợp.
- Duplicate event không tạo workflow hoặc artifact sai.
- Quyền IAM của dispatcher và consumer được giới hạn theo tài nguyên.
