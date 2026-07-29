---
title: "Nhật ký Tuần 2"
date: 2026-06-29
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

**Thời gian:** 29/06/2026 – 05/07/2026

## Mục tiêu Tuần 2

- Tìm hiểu lưu trữ Amazon S3 riêng tư và có versioning.
- Xây dựng luồng tải PDF trực tiếp từ trình duyệt lên S3 một cách an toàn.
- Thiết kế metadata và các trạng thái vòng đời tài liệu trong DynamoDB.
- Triển khai API tài liệu theo chủ sở hữu.
- Áp dụng tính idempotent và xóa dữ liệu an toàn.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| Đầu tuần | Tôi tìm hiểu S3 Block Public Access, mã hóa, versioning, quyền sở hữu đối tượng và các yếu tố về vòng đời dữ liệu. | FinSight AI lưu PDF trong bucket riêng tư, được mã hóa, có versioning và không cho phép truy cập đối tượng công khai. |
| Đầu tuần | Tôi học cách chính sách presigned POST có ràng buộc giới hạn kích thước, MIME type, object key và header mã hóa. | Luồng tải lên cho phép gửi PDF trực tiếp tới S3 nhưng backend vẫn kiểm soát mọi trường tải lên đáng tin cậy. |
| Giữa tuần | Tôi tìm hiểu cách kiểm tra file bằng chữ ký `%PDF-`, kích thước khai báo, metadata và tính toàn vẹn SHA-256. | Lambda xác nhận kiểm tra đối tượng đã tải lên trước khi chuyển tài liệu sang trạng thái đáng tin cậy. |
| Giữa tuần | Tôi học về partition key, sort key, cập nhật có điều kiện và trạng thái vòng đời rõ ràng trong DynamoDB. | Metadata tài liệu được lưu tách biệt với nội dung PDF và được phân vùng theo chủ sở hữu đã xác thực. |
| Cuối tuần | Tôi tìm hiểu kiểm tra request trong API Gateway và Lambda, tính idempotent, phân trang và xóa có nhận biết version. | Dự án triển khai API danh sách, chi tiết và xóa theo chủ sở hữu, hỗ trợ request lặp lại an toàn và phản hồi lỗi có cấu trúc. |

## Kết quả đạt được trong Tuần 2

- Triển khai tải PDF an toàn mà không công khai bucket hoặc đối tượng S3.
- Lưu metadata tài liệu tách biệt với nội dung PDF trong DynamoDB.
- Hoàn thành thao tác danh sách, chi tiết, phân trang và xóa theo chủ sở hữu.
- Ngăn truy cập tài liệu giữa các người dùng bằng cách suy ra chủ sở hữu từ ngữ cảnh request đã xác thực.
- Bổ sung tính idempotent cho tạo, xác nhận và xóa để retry an toàn.
- Kiểm tra luồng tải lên và quản lý tài liệu bằng test cục bộ và test tích hợp trên AWS.
- Rút ra bài học rằng bảo mật tải lên cần sự phối hợp giữa API Gateway, Lambda, IAM, DynamoDB và S3.
