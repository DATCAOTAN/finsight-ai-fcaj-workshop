---
title: "Workshop"
date: 2026-07-29
weight: 5
chapter: false
pre: " <b>5.</b> "
---

FinSight AI là ứng dụng serverless trên AWS, hỗ trợ tải PDF tài chính lên an toàn, trích xuất văn bản nhúng theo từng trang và tạo kết quả phân tích có cấu trúc kèm trích dẫn. Workshop này triển khai kiến trúc development đã được kiểm chứng tại **ap-southeast-1** và chủ động chọn **Google Gemini gemini-2.5-flash** làm nhà cung cấp phân tích.

## Kết quả học tập

Sau khi hoàn thành workshop, bạn có thể:

- kiểm tra source FinSight AI trên máy cục bộ;
- lưu Gemini API key trong AWS Secrets Manager mà không đưa key vào source control;
- triển khai backend và hạ tầng AWS bằng AWS SAM;
- build và phát hành frontend riêng tư qua CloudFront;
- đăng ký Cognito user đã xác nhận và phân tích PDF theo luồng end-to-end;
- kiểm tra phân tách theo owner, lưu trữ riêng tư, xử lý bất đồng bộ, giám sát và cleanup.

## Nội dung workshop

1. [Tổng quan](5.1-overview/)
2. [Điều kiện tiên quyết](5.2-prerequisites/)
3. [Kiến trúc](5.3-architecture/)
4. [Triển khai](5.4-deployment/)
5. [Demo end-to-end](5.5-demo/)
6. [Kiểm tra bảo mật và vận hành](5.6-verification/)
7. [Cleanup](5.7-cleanup/)

Workshop sử dụng các placeholder như **&lt;profile&gt;**, **&lt;exact-secret-arn&gt;** và **&lt;path-to-pdf&gt;**. Chỉ thay chúng trong terminal cục bộ và không commit giá trị thật.
