---
title: "Nhật ký Tuần 4"
date: 2026-07-13
weight: 4
---

**Thời gian:** 13–19/07/2026

## Mục tiêu Tuần 4

- Nghiên cứu AWS Step Functions để quy trình nhiều bước có thể quan sát và phục hồi.
- Hiểu cách gọi API có xác thực IAM và thiết kế vai trò dịch vụ theo nguyên tắc đặc quyền tối thiểu.
- Học cách xây dựng khả năng quan sát thực tế bằng log có cấu trúc, chỉ số, cảnh báo và kiểm tra sức khỏe.
- Củng cố ranh giới bảo mật cho hàng đợi, lưu trữ và thực thi quy trình.
- Chuẩn bị các bước kiểm tra vận hành có thể lặp lại cho triển khai và dọn dẹp.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| 13/07 | Tôi đã nghiên cứu cách điều phối quy trình giúp xử lý nhiều bước có thể quan sát và phục hồi. | Mô hình hóa các bước trích xuất, kiểm tra, phân tích và hoàn tất thành các trạng thái Step Functions với đường đi thành công và thất bại rõ ràng. |
| 14/07 | Tôi đã tìm hiểu API xác thực bằng IAM và AWS Signature Version 4. | Cấu hình API dùng cơ chế ủy quyền `AWS_IAM` cho các yêu cầu được bảo vệ. |
| 15/07 | Tôi đã học cách ranh giới đặc quyền tối thiểu giảm tác động khi một thành phần bị xâm phạm. | Thu hẹp quyền của Lambda, hàng đợi, bucket, bảng và quy trình xuống đúng hành động cùng tài nguyên mà từng thành phần cần. |
| 16–17/07 | Tôi đã nghiên cứu log có cấu trúc, chỉ số ứng dụng và vai trò của chúng trong khắc phục sự cố. | Bổ sung log có cấu trúc và bản ghi CloudWatch Embedded Metric Format cho trạng thái tài liệu, lỗi, độ trễ và hoạt động của nhà cung cấp phân tích. |
| 18–19/07 | Tôi đã học cách cảnh báo, kiểm tra sức khỏe, rà soát chi phí và dọn dẹp hỗ trợ khả năng sẵn sàng vận hành. | Bổ sung cảnh báo CloudWatch và kiểm tra sức khỏe, rà soát hành vi hàng đợi và chi phí, đồng thời thực hành dọn dẹp và quét thông tin bí mật. |

## Kết quả đạt được trong Tuần 4

- Thay chuỗi tác vụ nền ngầm định bằng quy trình Step Functions có thể quan sát tiến độ và lỗi.
- Bảo vệ các lượt gọi API của ứng dụng bằng xác thực IAM và Signature Version 4.
- Giảm các quyền dịch vụ quá rộng bằng cách gán vai trò có phạm vi hẹp cho từng thành phần xử lý.
- Bổ sung log vận hành có cấu trúc mà không đưa nội dung tài liệu hay thông tin đăng nhập vào thông điệp log.
- Xuất bản chỉ số về kết quả tài liệu, thời gian xử lý, lỗi hàng đợi và yêu cầu tới nhà cung cấp phân tích.
- Bổ sung cảnh báo CloudWatch cho lỗi xử lý, hàng đợi lỗi, thất bại quy trình và các điều kiện vận hành bất thường.
- Thiết lập các bước kiểm tra sức khỏe, nhận thức chi phí, quét thông tin bí mật và dọn dẹp để dùng trong giai đoạn xác thực sau.
