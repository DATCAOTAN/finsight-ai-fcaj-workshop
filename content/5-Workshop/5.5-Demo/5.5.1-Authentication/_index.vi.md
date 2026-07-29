---
title: "Xác thực"
date: 2026-07-29
weight: 1
chapter: false
pre: " <b>5.5.1.</b> "
---

1. Mở CloudFront URL được lưu trong **$WorkshopFrontendUrl**.
2. Chọn **Create account**.
3. Nhập email workshop có kiểm soát và password riêng đáp ứng policy hiển thị.
4. Gửi form. Tài khoản vẫn chưa xác nhận và chưa thể nhận AWS credential.

![Tạo tài khoản workshop có kiểm soát](/images/5-Workshop/5.5-Demo/create-account-form.png)

5. Đọc confirmation code từ mailbox có kiểm soát.
6. Chọn **Confirm email**, nhập cùng email và code rồi gửi.
7. Chọn **Sign in** và đăng nhập.

Sau khi đăng nhập, trình duyệt đổi Cognito token lấy Identity Pool credential ngắn hạn và chỉ giữ trong bộ nhớ để ký API request. Không kiểm tra, sao chép hoặc chụp token hay credential value.

## Kết quả mong đợi

- User chưa xác nhận không thể vào workspace riêng tư.
- User đã xác nhận thấy document list theo owner đang trống.
- Tải lại trang khôi phục Cognito session mà không lưu AWS credential dài hạn.

![Workspace của user đã xác nhận](/images/5-Workshop/5.5-Demo/confirmed-user-workspace.png)

![Danh sách tài liệu theo owner đang trống](/images/5-Workshop/5.5-Demo/document-list-empty.png)

Để kiểm tra isolation tùy chọn, tạo user có kiểm soát thứ hai và xác minh mỗi tài khoản chỉ thấy document list của chính mình. Không hiển thị Cognito identity ID thô.
