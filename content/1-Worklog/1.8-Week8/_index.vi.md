---
title: "Nhật ký Tuần 8"
date: 2026-08-10
publishDate: 2026-07-29
weight: 8
pre: " <b> 1.8. </b> "
---

**Thời gian:** 10–15/08/2026

## Mục tiêu Tuần 8

- Xác thực toàn trình các kiểm soát đăng nhập, cô lập quyền sở hữu và lưu trữ riêng tư.
- Xác nhận sức khỏe quy trình, cảnh báo, hành vi hàng đợi và phản hồi lỗi an toàn.
- Chạy đầy đủ bộ kiểm thử backend và frontend, đồng thời rà soát độ bao phủ.
- Kiểm tra hạ tầng đã triển khai và dọn dẹp tài nguyên xác thực tạm thời.
- Hoàn thiện tài liệu song ngữ về kiến trúc, cách sử dụng và quá trình học tập thực tập.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| 10/08 | Nghiên cứu kiểm thử phân quyền nhiều người dùng để xác minh khả năng cô lập chủ sở hữu. | Kiểm tra cô lập tài liệu bằng hai tài khoản và xác nhận truy cập chéo chủ sở hữu nhận phản hồi không tìm thấy an toàn. |
| 11/08 | Tìm hiểu cách kiểm thử bảo mật phủ định xác minh yêu cầu được bảo vệ và lưu trữ riêng tư. | Xác nhận yêu cầu API không ký và truy cập trực tiếp đối tượng S3 riêng tư đều bị từ chối, trong khi luồng thử lại đã xác thực vẫn sử dụng được. |
| 12/08 | Nghiên cứu cách log, lịch sử quy trình, hàng đợi, phản hồi sức khỏe và cảnh báo tạo ra các tín hiệu vận hành bổ trợ nhau. | Rà soát từng tín hiệu trong cả tình huống bình thường lẫn lỗi. |
| 13/08 | Tìm hiểu vì sao dọn dẹp là một phần của chu kỳ xác thực hoàn chỉnh. | Xóa tài liệu tạm, thông điệp hàng đợi, danh tính kiểm thử và các sản phẩm xác thực khác mà không ảnh hưởng đến tài nguyên ứng dụng đã triển khai. |
| 14/08 | Nghiên cứu cách số lượng kiểm thử và độ bao phủ hỗ trợ đánh giá chất lượng cuối cùng. | Chạy các bộ kiểm thử backend và frontend hiện hành, ghi nhận độ bao phủ rồi rà soát mọi lỗi hoặc cảnh báo còn lại. |
| 15/08 | Tìm hiểu cách tài liệu phát hành kết nối kiến trúc, vận hành, xác thực và bàn giao dự án. | Cập nhật kiến trúc và nội dung Hugo song ngữ, xác minh bản triển khai và thực hiện rà soát sẵn sàng phát hành cuối cùng. |

## Kết quả dự kiến trong Tuần 8

- Xác nhận khả năng cô lập chủ sở hữu bằng hai tài khoản có kiểm soát và phản hồi an toàn khi truy cập tài liệu không được phép.
- Xác minh yêu cầu được bảo vệ nhưng không ký và truy cập trực tiếp nội dung S3 riêng tư đều bị từ chối.
- Kiểm tra lại luồng thành công và luồng đầu vào vượt giới hạn dự kiến ở Tuần 7.
- Chạy các bộ kiểm thử backend và frontend hiện hành, đồng thời ghi nhận độ bao phủ.
- Xác minh tình trạng stack, quy trình, hàng đợi và cảnh báo CloudWatch.
- Dọn dẹp dữ liệu và tài nguyên xác thực tạm thời sau các bước kiểm tra cuối.
- Hoàn thiện nhật ký và tài liệu hỗ trợ song ngữ.
