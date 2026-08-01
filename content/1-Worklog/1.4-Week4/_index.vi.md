---
title: "Nhật ký Tuần 4"
date: 2026-07-13
weight: 4
pre: " <b> 1.4. </b> "
---

**Thời gian:** 13–19/07/2026

## Mục tiêu

- Điều phối quy trình trích xuất có trạng thái và khả năng phục hồi.
- Thu hẹp quyền IAM theo từng thành phần.
- Thiết lập log, metric và alarm vận hành.

## Tấn Đạt

### Kiến thức AWS

| Nội dung | Kiến thức đạt được |
|---|---|
| Step Functions | Hiểu Retry, Catch, trạng thái lỗi và cách phục hồi workflow nhiều bước. |
| IAM | Hiểu execution role, resource-level permission và phân tách quyền theo Lambda. |
| Amazon CloudWatch | Hiểu Logs, Embedded Metric Format, metric filter, alarm và evaluation window. |

### Công việc thực hiện

- Mô hình hóa các bước validate, extraction và failure handling trong state machine.
- Tách IAM role cho API, dispatcher, consumer và processing Lambda.
- Thêm log có cấu trúc, metric và alarm cho Lambda error, workflow failure, queue backlog và DLQ.

## Kết quả và bằng chứng

- Workflow khôi phục được lỗi tạm thời và ghi trạng thái thất bại có kiểm soát.
- IAM không có wildcard toàn cục; mỗi Lambda chỉ truy cập tài nguyên cần thiết.
- Alarm phản ứng với lỗi kiểm thử có chủ đích và tự trở lại `OK` khi evaluation window hết dữ liệu lỗi.
