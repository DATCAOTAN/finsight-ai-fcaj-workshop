---
title: "Tuần 4"
date: 2026-07-13
weight: 4
pre: " <b> 1.4. </b> "
---

**Thời gian:** 13–19/07/2026

## Mục tiêu Tuần 4

- Sử dụng CloudWatch để kiểm tra log, metric và alarm.
- Xây dựng regression test trên AWS cho các phase đã hoàn thành.
- Kiểm tra log không làm lộ dữ liệu nhạy cảm.
- Chuẩn hóa checklist vận hành và bằng chứng.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| 13/07 | Tìm hiểu CloudWatch Logs và Logs Insights. | Truy vấn lỗi theo document/request mà không ghi nội dung PDF hoặc credential. |
| 14/07 | Học CloudWatch Metrics, EMF và alarm evaluation. | Kiểm tra alarm cho Lambda, workflow, queue backlog và DLQ. |
| 15/07 | Tìm hiểu trạng thái OK, ALARM và INSUFFICIENT_DATA. | Xác nhận alarm do test lỗi có chủ đích tự trở lại OK. |
| 16–17/07 | Học AWS CLI để thu thập bằng chứng vận hành. | Kiểm tra stack status, queue attributes, alarm state và resource policy. |
| 18–19/07 | Nghiên cứu negative security testing. | Kiểm tra log không chứa credential, JWT, presigned URL đang hoạt động hoặc text tài liệu. |

## Kết quả đạt được trong Tuần 4

- Hoàn thành regression test cho upload, quản lý tài liệu, queue và extraction.
- Xác minh alarm phản ứng và tự hồi phục đúng evaluation window.
- Không phát hiện dữ liệu nhạy cảm trong log được kiểm tra.
- Hoàn thiện checklist stack, queue/DLQ, alarm, test và cleanup có kiểm soát.
