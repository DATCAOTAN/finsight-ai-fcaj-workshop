---
title: "Nhật ký Tuần 5"
date: 2026-07-20
weight: 5
---

**Thời gian:** 20–26/07/2026

## Mục tiêu Tuần 5

- Nghiên cứu Amazon Cognito User Pool và sự khác nhau giữa xác thực với phân quyền.
- Học cách trình duyệt gọi API được IAM bảo vệ mà không nhúng thông tin đăng nhập dài hạn.
- Xây dựng các hành trình React chính cho đăng nhập, tải lên và theo dõi tài liệu.
- Thực thi quyền sở hữu tài liệu ở phía máy chủ thay vì tin danh tính do trình duyệt gửi.
- Phân phối frontend qua S3 riêng tư và Amazon CloudFront.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| 20/07 | Tôi đã nghiên cứu xác thực Cognito và sự phân tách giữa User Pool, application client với thông tin đăng nhập AWS. | Cấu hình Cognito User Pool và application client cho người dùng đã xác thực, không đặt client secret trong trình duyệt và tắt truy cập chưa xác thực. |
| 21/07 | Tôi đã học cách trình duyệt dùng thông tin đăng nhập tạm thời để ký yêu cầu AWS an toàn. | Dùng thông tin đăng nhập Cognito tạm thời để ký các yêu cầu API được bảo vệ bằng Signature Version 4. |
| 22/07 | Tôi đã nghiên cứu sự khác nhau giữa xác thực, phân quyền và quyền sở hữu tài nguyên. | Lấy danh tính người dùng từ ngữ cảnh yêu cầu đã xác minh và áp dụng kiểm tra chủ sở hữu cho thao tác liệt kê, tải lên, xem trạng thái và xem kết quả. |
| 23–24/07 | Tôi đã tìm hiểu các mẫu tương tác React cho hành trình ứng dụng bất đồng bộ. | Xây dựng màn hình đăng nhập, danh sách tài liệu, tải lên, làm mới trạng thái cùng các trạng thái đang tải, rỗng, thành công và lỗi an toàn. |
| 25–26/07 | Tôi đã học cách CloudFront phân phối trang tĩnh trong khi S3 origin vẫn ở chế độ riêng tư. | Phân phối bản dựng React qua CloudFront với S3 origin riêng tư, sau đó kiểm tra luồng xác thực, quyền sở hữu và yêu cầu từ trình duyệt. |

## Kết quả đạt được trong Tuần 5

- Bổ sung đăng nhập bằng Cognito với thông tin đăng nhập AWS ngắn hạn cho phiên trình duyệt.
- Không đưa thông tin bí mật dài hạn hoặc client secret của ứng dụng vào frontend.
- Ký các yêu cầu từ trình duyệt tới API được IAM bảo vệ.
- Thực thi quyền sở hữu từ danh tính đã được máy chủ xác minh thay vì chấp nhận mã chủ sở hữu do client gửi.
- Hoàn thiện giao diện quản lý tài liệu cốt lõi, gồm tiến trình tải lên và phản hồi trạng thái dễ hiểu.
- Bổ sung trạng thái đang tải, rỗng và lỗi rõ ràng để các tình huống dự kiến không gây nhầm lẫn.
- Phân phối frontend qua CloudFront trong khi vẫn giữ S3 origin ở chế độ riêng tư.
