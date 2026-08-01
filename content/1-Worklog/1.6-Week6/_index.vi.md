---
title: "Nhật ký Tuần 6 - Tấn Đạt"
date: 2026-07-27
weight: 6
pre: " <b> 1.6. </b> "
---

**Thời gian:** 27/07–02/08/2026

## Mục tiêu Tuần 6

- Xây dựng Analysis Lambda và result API.
- Kiểm tra JSON schema và page citations.
- Lưu result artifact private và provenance an toàn.
- Bảo vệ provider credential bằng Secrets Manager.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| 27/07 | Tìm hiểu Bedrock InvokeModel, IAM và quota. | Giữ Bedrock là source/template default và ghi nhận live acceptance bị quota chặn. |
| 28/07 | Học AWS Secrets Manager và secret ARN policy. | Chỉ cấp Analysis Lambda quyền đọc selected provider key. |
| 29/07 | Nghiên cứu JSON schema validation. | Từ chối response thiếu trường hoặc sai kiểu trước khi lưu. |
| 30–31/07 | Học page-citation validation và provenance. | Kiểm tra citation nằm trong page range và lưu provider/model/version an toàn. |
| 01–02/08 | Tìm hiểu S3 result artifact và DynamoDB metadata. | Lưu full result trong S3; DynamoDB chỉ giữ trạng thái và metadata. |

## Kết quả đạt được trong Tuần 6

- Analysis Lambda giữ nguyên schema và citation contract.
- Response không hợp lệ không được đánh dấu `COMPLETED`.
- Result API dùng compound key theo owner và không lộ S3 key hoặc lỗi nội bộ.
- Secret không xuất hiện trong source, template, frontend hoặc log.
