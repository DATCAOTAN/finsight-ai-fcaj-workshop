---
title: "Nhật ký Tuần 7"
date: 2026-08-03
publishDate: 2026-07-29
weight: 7
---

**Thời gian:** 03–09/08/2026

**Trạng thái tại ngày 29/07/2026:** Dự kiến

## Mục tiêu Tuần 7

- Hoàn thiện luồng tự đăng ký và xác nhận email.
- Làm cho lỗi xử lý tài liệu dễ hiểu, có thể phục hồi và an toàn khi thử lại.
- Xác thực Gemini qua ranh giới provider hiện có trong môi trường phát triển.
- Rà soát ranh giới dữ liệu khi dùng dịch vụ phân tích bên ngoài.
- Kiểm tra luồng tài liệu dài thành công và luồng từ chối đầu vào vượt giới hạn.

## Nội dung học tập và công việc dự kiến

| Thời gian | Nội dung học tập dự kiến | Công việc dự kiến áp dụng vào FinSight AI |
|---|---|---|
| 03/08 | Tìm hiểu vòng đời đăng ký và xác nhận email của Cognito. | Rà soát tự đăng ký, xác nhận, gửi lại mã, hướng dẫn đăng nhập và cách xử lý tài khoản chưa xác nhận. |
| 04/08 | Tìm hiểu phản hồi xác thực an toàn. | Xác minh lỗi đăng ký và xác nhận dự kiến tạo thông báo hữu ích mà không tiết lộ chi tiết tài khoản nhạy cảm. |
| 05/08 | Tìm hiểu phân loại lỗi, thời gian chờ và giới hạn số lần thử. | Xác minh chỉ tài liệu lỗi đủ điều kiện mới có thể quay lại quy trình xử lý. |
| 06/08 | Tìm hiểu ranh giới tin cậy phát sinh khi dùng provider phân tích bên ngoài. | Xác thực luồng Gemini đã cấu hình và kiểm tra PDF gốc vẫn nằm trong vùng lưu trữ AWS riêng tư. |
| 07/08 | Tìm hiểu cơ chế bảo vệ kích thước đầu vào do máy chủ kiểm soát. | Xác nhận đầu vào quá lớn bị từ chối trước khi gọi provider, không cắt ngầm và không tự động chuyển provider. |
| 08–09/08 | Tìm hiểu kiểm tra biên bằng dữ liệu có tính đại diện. | Kiểm tra tài liệu dài và tài liệu vượt giới hạn, sau đó ghi nhận kết quả an toàn, có thể lặp lại. |

## Kết quả dự kiến của Tuần 7

- Rà soát luồng đăng ký và xác nhận với cách xử lý an toàn cho tài khoản chưa xác nhận.
- Xác minh hành vi retry đủ điều kiện với thời gian chờ và giới hạn số lần thử.
- Rà soát hành vi của Gemini trong môi trường phát triển qua ranh giới provider tường minh.
- Mô tả rõ cách xử lý dữ liệu bên ngoài: chỉ văn bản theo trang đã trích xuất và được tin cậy có thể rời AWS, còn PDF gốc vẫn riêng tư.
- Xác thực luồng đầu vào dài và quá lớn mà không trình bày kết quả một phần như kết quả hoàn chỉnh.

Không có hoạt động nào của Tuần 7 được báo cáo là đã hoàn thành tại ngày 29/07/2026.
