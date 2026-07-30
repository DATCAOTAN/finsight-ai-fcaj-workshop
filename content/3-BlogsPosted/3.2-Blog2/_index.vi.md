---
title: "Blog 2"
date: 2026-07-30
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Amazon S3 Express One Zone - Lưu trữ siêu tốc cho Database và Analytics

Thông thường chúng ta nghĩ đến Amazon S3 như một kho lưu trữ Object rẻ, bền bỉ nhưng tốc độ truy xuất thì ở mức "vừa phải". Tuy nhiên, sau khi đọc bài viết trên AWS Storage Blog về việc Turso (một database phân tán) sử dụng S3, mình đã phải thay đổi hoàn toàn suy nghĩ nhờ vào **Amazon S3 Express One Zone**.

### Sự khác biệt cốt lõi
**S3 Express One Zone** là một Storage Class mới được thiết kế đặc biệt cho các workload yêu cầu truy xuất dữ liệu liên tục với độ trễ ở mức **chữ số đơn của mili-giây (single-digit millisecond latency)**. 

Bài blog chia sẻ cách Turso đã dùng class này làm lớp lưu trữ (durability layer) cho transactional database của họ. Thay vì dùng ổ cứng EBS đắt đỏ hay EFS, họ ghi trực tiếp dữ liệu vào S3 Express One Zone và vẫn đạt được hiệu năng đáng kinh ngạc.

### Tại sao nó lại nhanh đến vậy?
* **Lưu trữ tại một Zone duy nhất:** Khác với S3 Standard lưu rải rác trên ít nhất 3 Availability Zones (AZs), Express One Zone chỉ lưu tại 1 AZ do bạn tự chọn. Việc này loại bỏ độ trễ truyền tải dữ liệu giữa các trung tâm dữ liệu.
* **Tối ưu hóa API:** Nó sử dụng một cơ chế xác thực riêng biệt (Session authentication) giúp tăng tốc độ gọi API lên rất nhiều lần.

Mặc dù việc chỉ lưu ở 1 AZ đồng nghĩa với rủi ro mất mát dữ liệu nếu Zone đó gặp thảm họa, nhưng S3 Express One Zone là sự thay thế hoàn hảo cho các giải pháp caching, xử lý dữ liệu AI/ML, hoặc tính toán tài chính (financial modeling) khi mà tốc độ là ưu tiên số một.

*Bài viết tham khảo: [How Turso built a transactional database using Amazon S3 Express One Zone](https://aws.amazon.com/blogs/storage/)*
