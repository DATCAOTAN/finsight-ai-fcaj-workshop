---
title: "Nhật ký Tuần 1"
date: 2026-06-22
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

**Thời gian:** 22/06/2026 – 28/06/2026

## Mục tiêu Tuần 1

- Hiểu yêu cầu dự án FCAJ và xác định bài toán của FinSight AI.
- Ôn lại kiến thức nền tảng AWS, mô hình trách nhiệm chung, IAM và nhận thức về chi phí.
- Tìm hiểu kiến trúc serverless và Infrastructure as Code.
- Thiết kế kiến trúc ban đầu để xử lý tài liệu tài chính an toàn.
- Chuẩn bị kho mã và môi trường phát triển AWS SAM.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| Đầu tuần | Tìm hiểu kết quả mong đợi của chương trình FCAJ và khó khăn khi phải xem xét thủ công các tài liệu tài chính dài. | Bài toán dự án tập trung vào tải lên an toàn, trích xuất tự động và phân tích tài chính có cấu trúc. |
| Đầu tuần | Học cách phạm vi dự án, người dùng mục tiêu, nội dung không thực hiện và độ nhạy dữ liệu định hướng quyết định kỹ thuật. | Dự án xác lập các ranh giới rõ ràng: tài liệu riêng tư, truy cập theo chủ sở hữu, không đưa ra khuyến nghị đầu tư và không bổ sung hạ tầng không cần thiết. |
| Giữa tuần | Tìm hiểu AWS Regions, mô hình trách nhiệm chung, IAM, đặc quyền tối thiểu và nhận thức về chi phí. | Các yêu cầu bảo mật và chi phí được đưa vào kiến trúc trước khi bắt đầu triển khai. |
| Giữa tuần | Thực hành hồ sơ AWS CLI và tìm hiểu cách AWS SAM cùng CloudFormation mô tả tài nguyên serverless dưới dạng mã. | Kho mã và môi trường phát triển SAM được chuẩn bị để kiểm tra và triển khai có thể lặp lại. |
| Cuối tuần | So sánh vai trò của API Gateway, Lambda, S3 và DynamoDB đối với API, xử lý, lưu trữ và metadata. | Kiến trúc FinSight AI ban đầu kết nối các dịch vụ này thành nền tảng xử lý tài liệu tài chính an toàn. |

## Kết quả đạt được trong Tuần 1

- Xác định bài toán, người dùng mục tiêu, phạm vi và nội dung không thực hiện của FinSight AI.
- Thiết kế kiến trúc serverless ban đầu cho quy trình xử lý tài liệu tài chính an toàn.
- Chuẩn bị AWS CLI, kho mã và môi trường phát triển AWS SAM.
- Xác lập lưu trữ riêng tư, truy cập theo chủ sở hữu, đặc quyền tối thiểu và log an toàn làm nguyên tắc bảo mật cốt lõi.
- Chia lộ trình thành tải lên an toàn, quản lý tài liệu, xử lý bất đồng bộ, trích xuất, phân tích, frontend và khả năng quan sát.
- Rút ra bài học rằng yêu cầu về bảo mật, chi phí và vòng đời tài nguyên cần được xác định trước khi triển khai.
