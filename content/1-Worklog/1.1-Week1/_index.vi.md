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

## Kết quả và bằng chứng

- Hoàn thành sơ đồ kiến trúc và phạm vi MVP.
- Xác định nguyên tắc owner-scoped access, không public tài liệu và không đưa ra khuyến nghị đầu tư.
- Repository có cấu trúc backend, infrastructure, tests và tài liệu rõ ràng.
