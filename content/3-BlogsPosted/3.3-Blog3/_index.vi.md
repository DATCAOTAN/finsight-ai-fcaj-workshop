---
title: "Blog 3"
date: 2026-07-30
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Vector Database trên AWS - Trái tim của ứng dụng Generative AI (RAG)

Khi tìm hiểu sâu về kiến trúc Generative AI trên AWS, mình nhận ra rằng các mô hình ngôn ngữ lớn (LLMs) dù thông minh đến đâu thì kiến thức của chúng cũng chỉ dừng lại ở thời điểm được huấn luyện (static data). Đọc qua loạt bài trên AWS Big Data Blog, mình xin đúc kết lại cách AWS giải quyết vấn đề này bằng mô hình **RAG (Retrieval-Augmented Generation)** kết hợp cùng **Vector Database**.

### Tại sao LLM lại cần Vector Database?
Để LLM trả lời được các câu hỏi liên quan đến dữ liệu nội bộ của công ty (ví dụ: chính sách nội bộ, báo cáo tài chính mới nhất), chúng ta phải dùng Vector Database. 
Hệ thống sẽ chuyển hóa văn bản thành các vector số học (embeddings) và lưu vào cơ sở dữ liệu. Khi user đặt câu hỏi, hệ thống sẽ thực hiện **tìm kiếm ngữ nghĩa (semantic search)** để lôi ra các tài liệu liên quan nhất, sau đó "mớm" ngữ cảnh đó cho LLM để nó trả lời chính xác và tránh bịa chuyện (hallucination).

### Các lựa chọn Vector DB trên AWS
Bài báo cũng điểm qua một số lựa chọn mà AWS cung cấp để lưu trữ Vector:
* **Amazon OpenSearch Service:** Phù hợp cho các doanh nghiệp cần scale lên hàng tỷ vectors với công cụ tìm kiếm mạnh mẽ.
* **Amazon RDS for PostgreSQL (với pgvector):** Đây là một extension tuyệt vời. Nếu bạn đã quen dùng PostgreSQL, bạn có thể biến nó thành Vector Database chỉ bằng vài câu lệnh SQL.
* **Amazon Bedrock Knowledge Bases:** Dịch vụ managed này gom tất cả quy trình RAG (nhúng dữ liệu, lưu trữ, truy xuất) lại làm một, giúp developer xây dựng ứng dụng GenAI chỉ trong vài cú click chuột.

Việc kết hợp LLM và Vector Search chắc chắn là tiêu chuẩn vàng (gold standard) để xây dựng ứng dụng AI trong doanh nghiệp ở thời điểm hiện tại.

*Bài viết tham khảo: [AWS Big Data / Generative AI Blogs](https://aws.amazon.com/blogs/big-data/)*
