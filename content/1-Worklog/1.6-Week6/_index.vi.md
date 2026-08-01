---
title: "Nhật ký Tuần 6"
date: 2026-07-27
weight: 6
pre: " <b> 1.6. </b> "
---

**Thời gian:** 27/07–02/08/2026

## Mục tiêu

- Tạo kết quả phân tích tài chính có schema và trích dẫn trang.
- Bảo vệ khóa API của provider và lưu provenance.
- Hoàn tất luồng lấy kết quả theo chủ sở hữu.

## Tấn Đạt

### Kiến thức AWS

| Nội dung | Kiến thức đạt được |
|---|---|
| AWS Secrets Manager | Hiểu secret ARN, IAM access, rotation boundary và không đưa secret vào log hoặc template. |
| Amazon Bedrock | Hiểu model invocation, quota tài khoản và vai trò source/template default của hệ thống. |
| S3 và DynamoDB | Hiểu tách result artifact khỏi metadata để tránh giới hạn item và giảm rò rỉ dữ liệu. |

### Công việc thực hiện

- Xây dựng Analysis Lambda với provider được chọn phía server, không cho trình duyệt chọn model.
- Kiểm tra JSON schema, trường bắt buộc và page citation trước khi chấp nhận kết quả.
- Lưu result artifact trong S3 private; chỉ lưu trạng thái, artifact key và provenance an toàn trong DynamoDB.

## Anh Đức

### Kiến thức AWS

| Nội dung | Kiến thức đạt được |
|---|---|
| Bedrock model access | Hiểu sự khác nhau giữa cấu hình model, quyền IAM và quota live của tài khoản. |
| Secrets Manager boundary | Hiểu chỉ Lambda được đọc secret; frontend không nhận provider key hoặc chọn provider. |
| CloudWatch provenance | Hiểu ghi provider/model/version an toàn để truy vết mà không lộ prompt hay dữ liệu tài liệu. |

### Công việc thực hiện

- Xây dựng giao diện kết quả gồm summary, metrics, risks, opportunities, citations và provenance.
- Hiển thị trạng thái processing/failed/completed nhất quán; không xem partial output là hoàn tất.
- Tạo test frontend cho schema result, page citations, thông báo an toàn và tài liệu không có kết quả.

## Kết quả và bằng chứng

- Kết quả sai schema hoặc citation bị từ chối, không được trình bày như phân tích hoàn tất.
- API result dùng owner-scoped compound key và không trả prompt, secret, S3 key hay lỗi nội bộ.
- Bedrock vẫn là source/template default; live acceptance bị chặn bởi quota tài khoản và không có automatic provider fallback.
