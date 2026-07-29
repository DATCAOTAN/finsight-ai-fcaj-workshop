---
title: "Triển khai"
date: 2026-07-29
weight: 4
chapter: false
pre: " <b>5.4.</b> "
---

[![Trình tự triển khai FinSight AI](/images/5-Workshop/5.4-Deployment/deployment-sequence.svg)](/images/5-Workshop/5.4-Deployment/deployment-sequence.svg)

*Hình: Trình tự triển khai SAM hai lượt và frontend.*

Quá trình triển khai gồm bốn giai đoạn:

1. [Kiểm tra source cục bộ](5.4.1-local-validation/)
2. [Lưu Gemini key an toàn](5.4.2-gemini-secret/)
3. [Triển khai AWS backend](5.4.3-backend/)
4. [Build và phát hành frontend](5.4.4-frontend/)

Lần SAM deploy đầu dùng frontend origin cục bộ để CloudFormation tạo distribution. Sau khi CloudFront trả về HTTPS URL, triển khai cùng stack lần thứ hai với chính xác origin đó. Bước này giúp API Gateway và S3 CORS chấp nhận trình duyệt đã triển khai.
