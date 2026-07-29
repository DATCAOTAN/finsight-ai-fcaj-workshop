---
title: "Nhật ký Tuần 6"
date: 2026-07-27
weight: 6
---

**Thời gian:** 27/07–02/08/2026

**Trạng thái tại ngày 29/07/2026:** Đang thực hiện

## Mục tiêu Tuần 6

- Xác định đầu ra có cấu trúc và ổn định cho việc phân tích tài liệu tài chính.
- Nghiên cứu kiểm tra schema, kiểm tra trích dẫn và giới hạn rõ ràng cho nội dung do AI tạo.
- Tách các tích hợp nhà cung cấp phân tích qua một ranh giới thống nhất.
- Bảo vệ thông tin xác thực của nhà cung cấp và ghi nhận nguồn gốc hữu ích mà không lộ bí mật.
- Trình bày kết quả phân tích rõ ràng nhưng không đưa ra khuyến nghị đầu tư.

## Nội dung học tập và công việc triển khai

| Thời gian | Trạng thái | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|---|
| 27/07 | Đã hoàn thành | Tôi đã nghiên cứu cách schema chuẩn giúp kết quả phân tích có AI trở nên ổn định cho các thành phần sử dụng phía sau. | Xác định các phần có cấu trúc cho tóm tắt, số liệu tài chính, rủi ro, cơ hội, trích dẫn và siêu dữ liệu phân tích. |
| 28/07 | Đã hoàn thành | Tôi đã học cách kiểm tra schema và trích dẫn cục bộ để loại bỏ sớm đầu ra không đáng tin cậy. | Bổ sung kiểm tra schema, kiểu dữ liệu, trường bắt buộc và trích dẫn theo trang trước khi chấp nhận kết quả phân tích. |
| 29/07 | Đã hoàn thành | Tôi đã nghiên cứu lớp trừu tượng nhà cung cấp và rủi ro của cơ chế chuyển đổi ngầm. | Giữ Amazon Bedrock làm mặc định trong mã nguồn và mẫu triển khai, giữ Groq dưới dạng lựa chọn phát triển không hoạt động và yêu cầu chọn provider rõ ràng. |
| 30–31/07 | Dự kiến | Tôi dự kiến tìm hiểu cách truy cập thông tin xác thực an toàn và tách kết quả khỏi siêu dữ liệu trạng thái. | Rà soát quyền truy cập bí mật của provider, lưu kết quả riêng tư và xử lý metadata an toàn. |
| 01–02/08 | Dự kiến | Tôi dự kiến tìm hiểu cách nguồn gốc, trích dẫn và tuyên bố giới hạn hỗ trợ việc trình bày phân tích có trách nhiệm. | Rà soát API kết quả và giao diện về nguồn gốc, tham chiếu trang và tuyên bố không đưa ra khuyến nghị đầu tư. |

## Kết quả Tuần 6 được ghi nhận đến ngày 29/07

- Thiết lập một định dạng phân tích chuẩn cho backend, lớp lưu trữ, kiểm thử và frontend.
- Bổ sung kiểm tra cục bộ để từ chối kết quả sai cấu trúc trước khi có thể hiển thị như phân tích hoàn chỉnh.
- Giữ tham chiếu trang để các nhận định quan trọng có thể được đối chiếu với văn bản trích xuất.
- Cô lập xử lý riêng của từng provider sau một ranh giới rõ ràng.
- Giữ việc chọn provider ở dạng tường minh và không có tự động chuyển đổi.

Các hoạt động còn lại của Tuần 6 là kế hoạch và không được báo cáo là đã hoàn thành.
