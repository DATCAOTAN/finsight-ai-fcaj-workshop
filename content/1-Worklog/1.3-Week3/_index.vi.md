---
title: "Nhật ký Tuần 3"
date: 2026-07-06
weight: 3
pre: " <b> 1.3. </b> "
---

**Thời gian:** 06–12/07/2026

## Mục tiêu Tuần 3

- Nghiên cứu xử lý hướng sự kiện với Amazon S3, EventBridge, Amazon SQS và AWS Lambda.
- Hiểu cơ chế thử lại, thời gian ẩn thông điệp, hàng đợi lỗi và xử lý idempotent.
- Học cách trích xuất văn bản nhúng trong PDF và đánh giá chất lượng theo từng trang.
- Xây dựng vòng đời xử lý tài liệu ổn định từ lúc tải lên đến khi có văn bản trích xuất.
- Giữ tệp tài liệu và sản phẩm trung gian ở chế độ riêng tư, chỉ công khai siêu dữ liệu an toàn.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| 06/07 | Nghiên cứu cách sự kiện S3 tạo thay đổi trạng thái mà không ghép nối trực tiếp các dịch vụ. | Kết nối lượt tải lên S3 đã được xác nhận với quy tắc EventBridge để quy trình chỉ bắt đầu sau khi đối tượng thực sự xuất hiện. |
| 07/07 | Tìm hiểu thời gian ẩn, cơ chế thử lại và hàng đợi lỗi của SQS để phân phối bất đồng bộ bền vững. | Cấu hình hàng đợi xử lý để hấp thụ tải đột biến và cô lập lỗi lặp lại. |
| 08/07 | Học vì sao consumer cần có tính idempotent khi thông điệp có thể được gửi nhiều lần. | Bổ sung kiểm tra vòng đời để thông điệp gửi trùng không khởi động lại tài liệu đang xử lý hoặc đã hoàn tất. |
| 09–10/07 | Nghiên cứu cách trích xuất văn bản nhúng trong PDF và giá trị của việc giữ ranh giới trang. | Dùng pypdf để lấy văn bản nhúng theo từng trang và giữ số trang cho phần trích dẫn sau này. |
| 11–12/07 | Học cách cổng kiểm tra chất lượng và sản phẩm riêng tư hỗ trợ xử lý tài liệu an toàn. | Bổ sung kiểm tra văn bản rỗng hoặc không sử dụng được, lưu nội dung trích xuất trong S3 riêng tư và chỉ giữ trạng thái cùng siêu dữ liệu sản phẩm trong DynamoDB. |

## Kết quả đạt được trong Tuần 3

- Hoàn thiện luồng hướng sự kiện từ lượt tải lên đã xác nhận đến hàng đợi xử lý tài liệu.
- Bổ sung cơ chế xử lý SQS có thử lại và hàng đợi lỗi cho các thông điệp thất bại nhiều lần.
- Làm cho consumer có tính idempotent để sự kiện trùng không tạo công việc trùng.
- Trích xuất văn bản nhúng trong PDF nhưng vẫn giữ ranh giới trang, tạo nền tảng cho phân tích có thể truy vết.
- Xử lý rõ ràng các PDF mã hóa, không đọc được, chỉ chứa ảnh hoặc có văn bản không sử dụng được thay vì âm thầm tạo kết quả kém.
- Giữ PDF gốc và sản phẩm trích xuất ở chế độ riêng tư trong S3, còn ứng dụng chỉ trả về thông tin trạng thái an toàn.
- Thiết lập các trạng thái tài liệu rõ ràng để API và giao diện ở giai đoạn sau có thể hiển thị nhất quán.
