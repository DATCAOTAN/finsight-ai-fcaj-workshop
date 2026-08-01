---
title: "Nhật ký Tuần 1"
date: 2026-06-22
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

**Thời gian:** 22–28/06/2026

## Mục tiêu

- Xác định bài toán, phạm vi và dữ liệu nhạy cảm của FinSight AI.
- Nắm nền tảng AWS và mô hình trách nhiệm chung.
- Thiết kế kiến trúc serverless ban đầu và môi trường Infrastructure as Code.

## Tấn Đạt

### Kiến thức AWS

| Nội dung | Kiến thức đạt được |
|---|---|
| AWS Global Infrastructure | Hiểu Region, Availability Zone và lý do chọn `ap-southeast-1`. |
| IAM và Shared Responsibility Model | Phân biệt trách nhiệm bảo mật của AWS và khách hàng; áp dụng đặc quyền tối thiểu. |
| AWS SAM và CloudFormation | Hiểu cách khai báo, kiểm tra và triển khai tài nguyên serverless có thể lặp lại. |

### Công việc thực hiện

- Phân tích luồng backend từ API Gateway, Lambda đến S3 và DynamoDB.
- Thiết kế ranh giới IAM, lưu trữ riêng tư và mã hóa làm yêu cầu từ đầu.
- Khởi tạo cấu trúc SAM/CloudFormation và quy trình kiểm tra template.

## Anh Đức

### Kiến thức AWS

| Nội dung | Kiến thức đạt được |
|---|---|
| AWS Well-Architected Framework | Hiểu sáu trụ cột và cách dùng bảo mật, độ tin cậy, chi phí để đánh giá MVP. |
| Serverless trên AWS | Hiểu vai trò của API Gateway, Lambda, S3 và DynamoDB trong kiến trúc không máy chủ. |
| AWS Pricing và Budgets | Hiểu mô hình pay-as-you-go, Free Tier và yêu cầu theo dõi chi phí từ đầu. |

### Công việc thực hiện

- Phân tích người dùng, hành trình upload–theo dõi–xem kết quả và tiêu chí demo.
- Xây dựng kế hoạch kiểm thử, danh mục bằng chứng và cấu trúc tài liệu workshop.
- Rà soát kiến trúc theo góc nhìn trải nghiệm người dùng, chi phí và khả năng vận hành.

## Kết quả và bằng chứng

- Hoàn thành sơ đồ kiến trúc và phạm vi MVP.
- Xác định nguyên tắc owner-scoped access, không public tài liệu và không đưa ra khuyến nghị đầu tư.
- Repository có cấu trúc backend, infrastructure, tests và tài liệu rõ ràng.
