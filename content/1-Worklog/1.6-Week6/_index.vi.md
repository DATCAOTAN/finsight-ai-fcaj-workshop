---
title: "Nhật ký Tuần 6"
date: 2026-07-27
weight: 6
---

**Thời gian:** 27/07–02/08/2026

## Mục tiêu Tuần 6

- Xác định đầu ra có cấu trúc và ổn định cho việc phân tích tài liệu tài chính.
- Nghiên cứu kiểm tra schema, kiểm tra trích dẫn và giới hạn rõ ràng cho nội dung do AI tạo.
- Tách các tích hợp nhà cung cấp phân tích qua một ranh giới thống nhất.
- Bảo vệ thông tin xác thực của nhà cung cấp và ghi nhận nguồn gốc hữu ích mà không lộ bí mật.
- Trình bày kết quả phân tích rõ ràng nhưng không đưa ra khuyến nghị đầu tư.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| 27/07 | Tôi đã nghiên cứu cách schema chuẩn giúp kết quả phân tích có AI trở nên ổn định cho các thành phần sử dụng phía sau. | Xác định các phần có cấu trúc cho tóm tắt, số liệu tài chính, rủi ro, cơ hội, trích dẫn và siêu dữ liệu phân tích. |
| 28/07 | Tôi đã học cách kiểm tra schema và trích dẫn cục bộ để loại bỏ sớm đầu ra không đáng tin cậy. | Bổ sung kiểm tra schema, kiểu dữ liệu, trường bắt buộc và trích dẫn theo trang trước khi chấp nhận một kết quả phân tích. |
| 29–30/07 | Tôi đã nghiên cứu lớp trừu tượng nhà cung cấp và rủi ro của cơ chế chuyển đổi ngầm. | Giữ Amazon Bedrock làm mặc định trong mã nguồn và mẫu triển khai, triển khai Groq dưới dạng lựa chọn phát triển không hoạt động, đồng thời không dùng cơ chế tự động chuyển nhà cung cấp. |
| 31/07 | Tôi đã tìm hiểu cách truy cập thông tin xác thực an toàn và tách kết quả khỏi siêu dữ liệu trạng thái. | Đọc thông tin xác thực của nhà cung cấp từ AWS Secrets Manager, lưu sản phẩm kết quả trong S3 riêng tư và chỉ giữ trạng thái cùng siêu dữ liệu sản phẩm trong DynamoDB. |
| 01–02/08 | Tôi đã học cách nguồn gốc, trích dẫn và tuyên bố giới hạn hỗ trợ việc trình bày phân tích có trách nhiệm. | Bổ sung API kết quả và giao diện React với thông tin nhà cung cấp, mô hình, tham chiếu trang và tuyên bố rõ rằng đầu ra chỉ mang tính thông tin, không phải tư vấn đầu tư. |

## Kết quả đạt được trong Tuần 6

- Thiết lập một định dạng phân tích chuẩn để backend, lớp lưu trữ, kiểm thử và frontend cùng sử dụng.
- Từ chối kết quả sai cấu trúc ngay tại ứng dụng trước khi có thể hiển thị như một phân tích hoàn tất.
- Giữ tham chiếu trang để người dùng có thể đối chiếu các nhận định quan trọng với văn bản trích xuất từ tài liệu.
- Cô lập xử lý yêu cầu và phản hồi riêng của từng nhà cung cấp sau một ranh giới rõ ràng.
- Giữ Bedrock làm mặc định trong mã nguồn và mẫu triển khai, còn Groq đã được triển khai nhưng không hoạt động; mọi thay đổi nhà cung cấp đều phải thực hiện rõ ràng và không có tự động chuyển đổi.
- Lưu sản phẩm phân tích ở chế độ riêng tư, chỉ trả kết quả đã được phân quyền cùng siêu dữ liệu nguồn gốc an toàn.
- Trình bày tóm tắt, số liệu, rủi ro và cơ hội như nội dung phân tích tài liệu, kèm tuyên bố rõ ràng rằng hệ thống không đưa ra khuyến nghị đầu tư.
