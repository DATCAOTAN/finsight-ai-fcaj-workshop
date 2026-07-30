---
title: "Các bài blogs đã đăng"
date: 2026-07-30
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Dưới đây là danh sách các bài blog kỹ thuật mà tôi đã viết và chia sẻ trên cộng đồng [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj). Thay vì chỉ chia sẻ dự án cá nhân, các bài viết này được đúc kết từ quá trình mình đọc, nghiên cứu các bài báo chuyên sâu trên AWS Blog và tóm tắt lại những kiến thức cốt lõi nhất cho cộng đồng.

### [Blog 1 - Khởi động AWS Lambda siêu tốc với tính năng SnapStart](3.1-Blog1/)
Một bài tóm tắt và đánh giá về giải pháp khắc phục độ trễ khởi động (cold-start) khét tiếng của AWS Lambda. Bài viết chia sẻ cách SnapStart sử dụng snapshot của microVM để tăng tốc độ chạy function lên gấp 10 lần, đặc biệt hữu ích cho môi trường Java, Python và .NET.

### [Blog 2 - Amazon S3 Express One Zone - Lưu trữ siêu tốc cho Database và Analytics](3.2-Blog2/)
Bài viết tham khảo case study của Turso trên AWS Storage Blog. Mình đã phân tích lý do tại sao một Storage Class như S3 Express One Zone với độ trễ mili-giây lại có thể được dùng làm lớp lưu trữ cho các cơ sở dữ liệu giao dịch khắt khe.

### [Blog 3 - Vector Database trên AWS - Trái tim của ứng dụng Generative AI (RAG)](3.3-Blog3/)
Một bài tổng hợp kiến thức từ AWS Big Data Blog về vai trò của Vector Database trong kỷ nguyên AI. Bài viết giải thích cơ chế RAG (Retrieval-Augmented Generation) và điểm qua các dịch vụ lưu trữ vector hàng đầu trên AWS như OpenSearch, pgvector và Bedrock Knowledge Bases.
