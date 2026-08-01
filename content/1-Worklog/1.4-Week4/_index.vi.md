---
title: "Nhật ký Tuần 4 - Tấn Đạt"
date: 2026-07-13
weight: 4
pre: " <b> 1.4. </b> "
---

**Thời gian:** 13–19/07/2026

## Mục tiêu Tuần 4

- Điều phối validate và extraction bằng Step Functions.
- Thiết kế retry, catch và trạng thái lỗi có thể phục hồi.
- Tách IAM role theo từng Lambda.
- Thiết lập CloudWatch logs, metrics và alarms.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| 13/07 | Học Task, Retry, Catch và terminal state của Step Functions. | Mô hình hóa validate, extraction và failure handling trong state machine. |
| 14/07 | Tìm hiểu Lambda execution role và resource-level permission. | Tách role cho API, dispatcher, consumer và processing tasks. |
| 15/07 | Học structured logging và correlation field. | Ghi log theo document/workflow mà không chứa nội dung hoặc credential. |
| 16–17/07 | Nghiên cứu CloudWatch EMF và metric filters. | Phát metric cho lỗi Lambda, workflow và extraction. |
| 18–19/07 | Học CloudWatch alarm và evaluation window. | Tạo alarm cho error, queue backlog, DLQ và workflow failure. |

## Kết quả đạt được trong Tuần 4

- Workflow có retry giới hạn và đường failure rõ ràng.
- Không có IAM wildcard toàn cục; mỗi Lambda chỉ có quyền cần thiết.
- CloudWatch cung cấp log, metric và alarm cho các điểm lỗi chính.
- Alarm do test lỗi có chủ đích tự trở lại `OK` sau evaluation window.
