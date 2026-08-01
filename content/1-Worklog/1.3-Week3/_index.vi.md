---
title: "Nhật ký Tuần 3 - Anh Đức"
date: 2026-07-06
weight: 3
pre: " <b> 1.3. </b> "
---

**Thời gian:** 06–12/07/2026

## Mục tiêu Tuần 3

- Hiểu hoạt động của SQS, DLQ và Step Functions từ góc nhìn theo dõi xử lý.
- Trích xuất embedded text theo từng trang PDF.
- Đánh giá chất lượng extraction và xác định `requires_ocr`.
- Lưu artifact lớn trong S3 thay vì DynamoDB hoặc workflow state.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| 06/07 | Tìm hiểu message visibility, in-flight message và DLQ của SQS. | Xác định trạng thái giao diện phù hợp khi tài liệu đang chờ hoặc xử lý lỗi. |
| 07/07 | Học cách đọc execution history trong Step Functions. | Theo dõi tài liệu qua validate, extraction và các nhánh failure. |
| 08/07 | Nghiên cứu trích xuất embedded text và giới hạn của PDF scan. | Triển khai lấy text theo trang, giữ đúng page number. |
| 09–10/07 | Học mô hình S3 artifact và giới hạn kích thước item/state. | Tạo extraction artifact JSON trong S3; DynamoDB chỉ giữ metadata. |
| 11–12/07 | Nghiên cứu quality gate cho dữ liệu trích xuất. | Tính số trang có text, tổng ký tự, coverage và cờ `requires_ocr`. |

## Kết quả đạt được trong Tuần 3

- Trích xuất và giữ đúng số trang cho PDF có embedded text.
- Tạo artifact extraction riêng tư trong S3.
- Đánh dấu rõ tài liệu thiếu text thay vì tạo kết quả sai.
- Hoàn thành test cho PDF hợp lệ, rỗng, malformed, encrypted và chỉ chứa ảnh.
