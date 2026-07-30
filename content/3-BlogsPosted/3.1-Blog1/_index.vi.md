---
title: "Blog 1"
date: 2026-07-30
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Khởi động AWS Lambda siêu tốc với tính năng SnapStart

Hôm nay mình vừa đọc được một series bài viết rất hay trên AWS Compute Blog về **AWS Lambda SnapStart** và muốn tóm tắt lại vài ý chính cho mọi người. Nếu hệ thống Serverless của bạn đang bị ảnh hưởng bởi độ trễ khởi động (cold-start latency) thì đây chính là "cứu cánh".

### SnapStart là gì và hoạt động thế nào?
Thay vì phải khởi tạo môi trường (init) từ đầu mỗi khi một Lambda function mới được gọi (cold-start), SnapStart sẽ chạy quá trình khởi tạo một lần khi bạn publish version mới của function. Sau đó, nó chụp một bức ảnh toàn cảnh (snapshot) bộ nhớ và trạng thái của microVM (sử dụng công nghệ Firecracker). 

Khi có request mới đến, Lambda chỉ việc "resume" lại từ snapshot này. Nhờ vậy, thời gian khởi động có thể **nhanh hơn gấp 10 lần**!

### Một số lưu ý mình rút ra từ bài báo:
* **Hỗ trợ đa ngôn ngữ:** Ban đầu SnapStart chỉ hỗ trợ Java (vốn nổi tiếng khởi động chậm), nhưng gần đây AWS đã mở rộng hỗ trợ cho cả **Python và .NET**.
* **Statefulness:** Vì SnapStart resume lại từ một trạng thái đã được lưu, các đoạn code sinh số ngẫu nhiên (randomness) hay khởi tạo connection đặc thù cần phải được xử lý khéo léo để đảm bảo tính duy nhất.
* **Không mất thêm phí:** Điều tuyệt vời là tính năng này hoàn toàn miễn phí. Bạn chỉ trả tiền cho dung lượng lưu trữ snapshot và thời gian thực thi như bình thường.

Nếu dự án của mọi người yêu cầu độ trễ cực thấp (latency-sensitive) thì việc cấu hình SnapStart qua AWS SAM hay Terraform là một thủ thuật cực kỳ đáng thử nghiệm!

*Bài viết tham khảo: [Starting up faster with AWS Lambda SnapStart](https://aws.amazon.com/blogs/compute/starting-up-faster-with-aws-lambda-snapstart/)*
