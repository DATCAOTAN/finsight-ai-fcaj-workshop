---
title: "Tuần 6"
date: 2026-07-27
weight: 6
pre: " <b> 1.6. </b> "
---

**Thời gian:** 27/07–02/08/2026

## Mục tiêu Tuần 6

- Hiểu ranh giới Amazon Bedrock, provider bên ngoài và Secrets Manager.
- Trình bày kết quả có cấu trúc và page citations.
- Không hiển thị partial output hoặc lỗi provider thô như kết quả hoàn tất.
- Kiểm tra provenance và thông báo an toàn.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| 27/07 | Tìm hiểu Bedrock model access, IAM permission và account quota. | Ghi đúng Bedrock là source/template default nhưng live acceptance bị quota chặn. |
| 28/07 | Học ranh giới AWS Secrets Manager. | Xác nhận chỉ Analysis Lambda đọc secret; frontend không nhận provider key. |
| 29/07 | Nghiên cứu JSON schema và page-citation validation. | Xây dựng giao diện theo schema đã kiểm tra thay vì đọc phản hồi provider tự do. |
| 30–31/07 | Học cách lưu provenance an toàn. | Hiển thị provider, model và citation nhưng không lộ prompt, S3 key hoặc exception. |
| 01–02/08 | Nghiên cứu trạng thái kết quả bất đồng bộ. | Phân biệt processing, failed và completed; không trình bày partial result là hoàn tất. |

## Kết quả đạt được trong Tuần 6

- Hoàn thiện giao diện summary, metrics, risks, opportunities và citations.
- Chỉ hiển thị kết quả đã vượt schema và citation validation.
- Không cho trình duyệt chọn provider hoặc model.
- Hoàn thành test cho result hợp lệ, lỗi an toàn và tài liệu chưa có kết quả.
