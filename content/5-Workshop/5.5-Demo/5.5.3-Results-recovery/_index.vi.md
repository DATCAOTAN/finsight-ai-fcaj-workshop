---
title: "Kết quả và recovery"
date: 2026-07-29
weight: 3
chapter: false
pre: " <b>5.5.3.</b> "
---

## Kết quả thành công

Khi trạng thái đạt **ANALYZED**, hãy kiểm tra:

- tổng quan và các chỉ số tài chính chính;
- xu hướng, rủi ro, bất thường và giới hạn;
- citation theo trang có thể đối chiếu với PDF nguồn;
- provenance của extraction và analysis;
- thông tin provider và model cho biết Gemini gemini-2.5-flash;
- disclaimer về phân tích tài chính.

Kết quả phải tóm tắt tài liệu nguồn mà không bịa số liệu hoặc cung cấp lời khuyên đầu tư cá nhân.

![Kết quả phân tích có cấu trúc](/images/5-Workshop/5.5-Demo/analysis-result-summary.png)

![Chỉ số, rủi ro và citation theo trang](/images/5-Workshop/5.5-Demo/analysis-citations-provider.png)

## Hành vi lỗi có kiểm soát

Nếu analysis kết thúc ở **ANALYSIS_FAILED**:

1. Đọc failure category đã được làm sạch trên UI.
2. Không sửa DynamoDB hoặc gửi lại queue message.
3. Nếu UI đánh dấu lỗi có thể retry, chờ hết cooldown hiển thị và chọn **Retry analysis** một lần.
4. Nếu input quá lớn hoặc không phù hợp, sử dụng PDF có văn bản ngắn hơn.

Hệ thống không tự động đổi từ Gemini sang provider khác.

## Xóa tài liệu workshop

Sau khi tài liệu đạt terminal state, chọn **Delete document** và xác nhận. Ứng dụng xóa artifact và version thuộc owner qua API được bảo vệ. Nếu hệ thống vẫn đang xử lý, thao tác xóa trả conflict; hãy chờ terminal state thay vì sửa record backend.
