---
title: "Tổng quan"
date: 2026-07-29
weight: 1
chapter: false
pre: " <b>5.1.</b> "
---

## Bối cảnh

[![Luồng Workshop FinSight AI end-to-end](/images/5-Workshop/5.1-Overview/workshop-end-to-end-flow.svg)](/images/5-Workshop/5.1-Overview/workshop-end-to-end-flow.svg)

*Hình: Luồng triển khai, demo, kiểm tra và cleanup FinSight AI.*

Bạn sẽ triển khai một môi trường development có kiểm soát cho FinSight AI. User đã xác nhận đăng nhập qua Amazon Cognito, tải lên một PDF tài chính có văn bản nhúng và nhận kết quả phân tích có cấu trúc từ Gemini mà không làm lộ bucket tài liệu hoặc AWS credential dài hạn cho trình duyệt.

Workshop đi theo một luồng hoàn chỉnh:

1. Kiểm tra ứng dụng trên máy cục bộ.
2. Tạo secret Gemini chuyên dụng.
3. Triển khai SAM stack.
4. Cấu hình CORS theo CloudFront URL vừa tạo.
5. Build và phát hành React frontend.
6. Xác nhận tài khoản Cognito và đăng nhập.
7. Tải lên, xử lý, xem kết quả, retry khi cần và xóa một PDF không nhạy cảm.
8. Kiểm tra queue, workflow, alarm và lưu trữ riêng tư.

## Giới hạn đã triển khai

- Cấu hình development giới hạn file tải lên ở 10 MiB.
- Bộ trích xuất hiện tại đọc văn bản nhúng trong PDF; hệ thống chưa chạy OCR hoặc Amazon Textract.
- Gemini nhận văn bản theo trang đã được tin cậy và metadata có giới hạn, không nhận file PDF gốc.
- Backend chọn provider; trình duyệt không thể đổi provider.
- Hệ thống không tự động fallback.
- Kết quả là phân tích tài liệu tài chính, không phải lời khuyên đầu tư.

## Thời gian và chi phí

Lần triển khai đầu tiên cần khoảng 90–120 phút. Stack dùng dịch vụ serverless tính phí theo mức sử dụng và không có compute chạy liên tục. Log, alarm, phiên bản S3, lưu lượng CloudFront và Gemini vẫn có thể phát sinh chi phí, vì vậy hãy hoàn thành phần cleanup khi không còn cần môi trường.
