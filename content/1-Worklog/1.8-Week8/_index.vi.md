---
title: "Nhật ký Tuần 8"
date: 2026-08-10
publishDate: 2026-07-29
weight: 8
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
| 10/08 | Tôi đã nghiên cứu kiểm thử phân quyền nhiều người dùng để xác minh khả năng cô lập chủ sở hữu. | Kiểm tra cô lập tài liệu bằng hai tài khoản và xác nhận truy cập chéo chủ sở hữu nhận phản hồi không tìm thấy an toàn. |
| 11/08 | Tôi đã học cách kiểm thử bảo mật phủ định xác minh yêu cầu được bảo vệ và lưu trữ riêng tư. | Xác nhận yêu cầu API không ký và truy cập trực tiếp đối tượng S3 riêng tư đều bị từ chối, trong khi luồng thử lại đã xác thực vẫn sử dụng được. |
| 12/08 | Tôi đã nghiên cứu cách log, lịch sử quy trình, hàng đợi, phản hồi sức khỏe và cảnh báo tạo ra các tín hiệu vận hành bổ trợ nhau. | Rà soát từng tín hiệu trong cả tình huống bình thường lẫn lỗi. |
| 13/08 | Tôi đã học vì sao dọn dẹp là một phần của chu kỳ xác thực hoàn chỉnh. | Xóa tài liệu tạm, thông điệp hàng đợi, danh tính kiểm thử và các sản phẩm xác thực khác mà không ảnh hưởng đến tài nguyên ứng dụng đã triển khai. |
| 14/08 | Tôi đã nghiên cứu cách số lượng kiểm thử và độ bao phủ hỗ trợ đánh giá chất lượng cuối cùng. | Chạy 288 kiểm thử backend với độ bao phủ 86% và 22 kiểm thử frontend, sau đó rà soát các lỗi cùng cảnh báo còn lại. |
| 15/08 | Tôi đã học cách tài liệu phát hành kết nối kiến trúc, vận hành, xác thực và bàn giao dự án. | Cập nhật kiến trúc và nội dung Hugo song ngữ, xác minh bản triển khai và thực hiện danh sách kiểm tra sẵn sàng phát hành cuối cùng. |

## Kết quả đạt được trong Tuần 8

- Xác nhận khả năng cô lập chủ sở hữu bằng hai tài khoản và phản hồi an toàn khi truy cập tài liệu không được phép.
- Xác minh yêu cầu được bảo vệ nhưng không ký và truy cập trực tiếp nội dung S3 riêng tư đều bị từ chối đúng thiết kế.
- Xác nhận lại hai kết quả biên ở Tuần 7: tài liệu 214.091 ký tự đạt trạng thái `ANALYZED` với một yêu cầu Gemini, còn tài liệu 1.368.551 ký tự trả về `ANALYSIS_INPUT_TOO_LARGE` mà không có yêu cầu nào tới nhà cung cấp.
- Hoàn tất 288 kiểm thử backend với độ bao phủ 86% và 22 kiểm thử frontend.
- Xác minh stack triển khai ở trạng thái `UPDATE_COMPLETE` với 73 tài nguyên hoạt động ổn định và cả 10 cảnh báo CloudWatch ở trạng thái `OK`.
- Dọn dẹp dữ liệu và tài nguyên xác thực tạm thời sau các bước kiểm tra cuối.
- Hoàn thiện nhật ký cùng tài liệu hỗ trợ song ngữ, mô tả chính xác kiến trúc là hạ tầng trên AWS kết hợp với nhà cung cấp Gemini bên ngoài trong môi trường phát triển, không phải giải pháp thuần AWS.
