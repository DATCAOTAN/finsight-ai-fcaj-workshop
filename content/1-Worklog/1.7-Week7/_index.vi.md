---
title: "Tuần 7–8"
date: 2026-08-03
publishDate: 2026-07-29
weight: 7
pre: " <b> 1.7. </b> "
---

**Thời gian:** 03–15/08/2026

## Mục tiêu Tuần 7–8

- Hoàn thiện self-registration và xác nhận email bằng Cognito.
- Cung cấp UX lỗi phân tích rõ ràng, an toàn và có hành động phù hợp.
- Xác nhận CloudFront đang phục vụ đúng production build.
- Hoàn thiện workshop, sơ đồ, bằng chứng và hướng dẫn demo.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| 03–04/08 | Tìm hiểu Cognito sign-up, confirmation code và resend code. | Hoàn thiện đăng ký, xác nhận email và xử lý mã sai bằng thông báo an toàn. |
| 05–06/08 | Học phân loại lỗi transient và non-retryable. | Hiển thị lỗi input, provider payload, rate limit, unavailable và unknown bằng thông báo tiếng Việt. |
| 07–09/08 | Nghiên cứu retry cooldown và duplicate-submit prevention. | Vô hiệu hóa nút retry khi request đang chạy và giữ tài liệu để retry hoặc xóa. |
| 10–12/08 | Tìm hiểu CloudFront invalidation và release verification. | Kiểm tra asset production, phiên đăng nhập cũ và người dùng đăng ký mới trên website thật. |
| 13–15/08 | Học cách trình bày kiến trúc và bằng chứng FCAJ. | Hoàn thiện Hugo song ngữ, sơ đồ AWS, ảnh bằng chứng, hướng dẫn demo và Worklog. |

## Kết quả đạt được trong Tuần 7–8

- Luồng đăng ký, xác nhận email, đăng nhập và đăng nhập lại được kiểm tra trên production.
- Lỗi phân tích nêu rõ upload/extraction đã thành công, chưa có kết quả hoàn chỉnh và hành động tiếp theo.
- Tài liệu dài được hướng dẫn chia theo phần logic; không khuyến nghị nén ảnh để giảm extracted-text token.
- Frontend production, browser acceptance và tài liệu Hugo vượt final gate.
- Tài liệu workshop phản ánh đúng runtime, provider và giới hạn đã kiểm chứng.
