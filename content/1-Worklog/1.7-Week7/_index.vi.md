---
title: "Nhật ký Tuần 7"
date: 2026-08-03
publishDate: 2026-07-29
weight: 7
---

**Thời gian:** 03–09/08/2026

## Mục tiêu Tuần 7

- Hoàn thiện luồng tự đăng ký và xác nhận email.
- Làm cho lỗi xử lý tài liệu dễ hiểu, có thể phục hồi và an toàn khi thử lại.
- Kích hoạt Gemini qua ranh giới nhà cung cấp hiện có để xác thực trong môi trường phát triển.
- Xác định và thực thi ranh giới dữ liệu khi dùng dịch vụ phân tích bên ngoài.
- Kiểm tra cả luồng thành công với tài liệu dài và luồng từ chối đầu vào vượt giới hạn.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| 03/08 | Tôi đã nghiên cứu vòng đời đăng ký và xác nhận email của Cognito. | Bổ sung tự đăng ký Cognito, xác nhận email, gửi lại mã và hướng dẫn đăng nhập, đồng thời vẫn chặn tài khoản chưa xác nhận. |
| 04/08 | Tôi đã học cách phản hồi xác thực vẫn hữu ích mà không tiết lộ chi tiết tài khoản nhạy cảm. | Ánh xạ các lỗi đăng ký và xác nhận thường gặp thành thông báo an toàn, dễ hiểu. |
| 05/08 | Tôi đã nghiên cứu phân loại lỗi, thời gian chờ và giới hạn số lần thử để phục hồi có kiểm soát. | Phân loại lỗi xử lý và chỉ cho phép tài liệu lỗi đủ điều kiện quay lại quy trình. |
| 06/08 | Tôi đã tìm hiểu ranh giới tin cậy phát sinh khi nhà cung cấp bên ngoài phân tích dữ liệu ứng dụng. | Kích hoạt Gemini gemini-2.5-flash qua lớp trừu tượng nhà cung cấp và xác minh PDF gốc vẫn nằm trong AWS; chỉ văn bản theo trang đã trích xuất và được tin cậy mới được gửi đi phân tích. |
| 07/08 | Tôi đã học vì sao giới hạn đầu vào phải được thực thi trước khi gửi yêu cầu tới nhà cung cấp. | Thực thi giới hạn phân tích 1.000.000 ký tự, từ chối rõ ràng thay vì cắt ngầm hoặc tự động chuyển nhà cung cấp. |
| 08–09/08 | Tôi đã nghiên cứu cách kiểm tra ranh giới bằng tài liệu dài và tài liệu vượt giới hạn có tính đại diện. | Chạy tài liệu 214.091 ký tự qua đúng một yêu cầu Gemini và kiểm tra tài liệu 1.368.551 ký tự bị từ chối trước khi phát sinh bất kỳ yêu cầu nào tới nhà cung cấp. |

## Kết quả đạt được trong Tuần 7

- Hoàn thiện các bước đăng ký, xác nhận, gửi lại mã và chuyển sang đăng nhập, đồng thời xử lý an toàn tài khoản chưa xác nhận.
- Bổ sung thông báo lỗi dễ hiểu cho các tình huống xác thực và đăng ký dự kiến.
- Thiết lập cơ chế phục hồi có kiểm soát cho lỗi tài liệu đủ điều kiện, kèm thời gian chờ và giới hạn số lần thử.
- Kích hoạt Gemini gemini-2.5-flash làm nhà cung cấp phân tích trong môi trường phát triển mà không thay đổi cơ chế chọn nhà cung cấp rõ ràng hay thêm tự động chuyển đổi.
- Giữ PDF gốc trong AWS và chỉ truyền văn bản theo trang đã trích xuất, được tin cậy ra bên ngoài, qua đó làm rõ kiến trúc kết hợp AWS và Gemini.
- Xử lý thành công tài liệu 214.091 ký tự đến trạng thái ANALYZED với đúng một yêu cầu tới Gemini.
- Từ chối tài liệu 1.368.551 ký tự với trạng thái ANALYSIS_INPUT_TOO_LARGE và không phát sinh yêu cầu nào tới nhà cung cấp, xác nhận đầu vào quá lớn không bị cắt hoặc gửi ra ngoài.
