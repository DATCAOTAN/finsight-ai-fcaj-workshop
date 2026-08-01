---
title: "Tuần 7–8"
date: 2026-08-03
publishDate: 2026-07-29
weight: 7
pre: " <b> 1.7. </b> "
---

**Thời gian:** 03–15/08/2026

## Mục tiêu Tuần 7–8

- Kích hoạt provider development qua ranh giới server-side.
- Phân loại lỗi phân tích và giới hạn retry đúng nguyên nhân.
- Kiểm tra security, stack, queue, alarm và log toàn trình.
- Hoàn thiện bằng chứng vận hành và kế hoạch cleanup.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| 03–04/08 | Tìm hiểu provider egress và Secrets Manager runtime access. | Kích hoạt Gemini development; giữ Bedrock default và không automatic fallback. |
| 05–06/08 | Học phân biệt local input limit, provider payload và rate limit. | Ánh xạ category ổn định; không suy ra PDF quá dài chỉ từ HTTP status. |
| 07–09/08 | Nghiên cứu bounded retry và idempotent recovery. | Chỉ retry lỗi transient; không retry payload quá lớn và không cắt input ngầm. |
| 10–12/08 | Học CloudFormation stack lifecycle và AWS security verification. | Kiểm tra stack, IAM, S3 private, unsigned request và cross-owner matrix. |
| 13–15/08 | Nghiên cứu queue/alarm health, cost evidence và cleanup. | Xác nhận queue/DLQ sạch, alarm OK, ghi chi phí trung thực và hoãn cleanup phá hủy đến sau demo. |

## Kết quả dự kiến trong Tuần 7–8

- Luồng upload, extraction, analysis và result hoạt động toàn trình với provider development được chọn phía server.
- Input vượt giới hạn bị từ chối trước provider; không cắt ngầm và không retry sai loại lỗi.
- Stack, IAM, S3, ownership, queue/DLQ, CloudWatch và secret scan vượt final gate.
- Bedrock vẫn là source/template default; live acceptance tiếp tục bị quota tài khoản chặn.
- Main stack được giữ cho demo; destructive cleanup chỉ thực hiện khi kết thúc môi trường.
