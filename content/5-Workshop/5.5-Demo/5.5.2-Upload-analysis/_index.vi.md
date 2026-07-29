---
title: "Tải lên và phân tích"
date: 2026-07-29
weight: 2
chapter: false
pre: " <b>5.5.2.</b> "
---

## Chọn tài liệu

Sử dụng PDF có văn bản nhúng, nhỏ hơn 10 MiB. Tài liệu phải không nhạy cảm và không chứa secret, dữ liệu cá nhân, dữ liệu khách hàng thật hoặc chỉ dẫn nhằm thao túng model.

1. Chọn control upload trong workspace riêng tư.
2. Chọn PDF.

![Chọn PDF không nhạy cảm](/images/5-Workshop/5.5-Demo/pdf-selected-for-upload.png)

3. Quan sát tiến độ upload.

![Tiến độ tải PDF lên](/images/5-Workshop/5.5-Demo/pdf-upload-progress.png)

4. Chờ tài liệu xuất hiện trong list theo owner.
5. Mở phần chi tiết tài liệu.

## Quan sát trạng thái bất đồng bộ

Luồng bình thường là:

**PENDING_UPLOAD → UPLOADED → QUEUED → EXTRACTING → EXTRACTED → ANALYZING → ANALYZED**

Trình duyệt polling theo khoảng thời gian có giới hạn. Không liên tục tải lại cùng tài liệu hoặc refresh quá mức khi hệ thống đang xử lý.

![Hệ thống đang phân tích tài liệu](/images/5-Workshop/5.5-Demo/document-processing-state.png)

## Hoạt động phía sau giao diện

- Backend sinh object key và upload form có ràng buộc.
- S3 nhận PDF mà không mở public.
- Bước confirm kiểm tra kích thước, metadata, chữ ký PDF và SHA-256.
- DynamoDB Streams và SQS khởi chạy Step Functions workflow đúng một lần.
- Bộ trích xuất giữ ranh giới từng trang.
- Gemini phân tích extraction đáng tin cậy.
- Backend kiểm tra schema và citation trước khi lưu kết quả.

Nếu tài liệu có quá ít văn bản nhúng, kết quả có thể báo trung thực rằng cần OCR. Không mô tả trường hợp này như OCR đã thành công.
