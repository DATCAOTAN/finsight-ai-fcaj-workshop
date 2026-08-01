---
title: "Nhật ký Tuần 2"
date: 2026-06-29
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

**Thời gian:** 29/06–05/07/2026

## Mục tiêu

- Xây dựng luồng tải PDF an toàn vào Amazon S3.
- Thiết kế metadata và vòng đời tài liệu trong DynamoDB.
- Cung cấp API quản lý tài liệu theo chủ sở hữu.

## Tấn Đạt

### Kiến thức AWS

| Nội dung | Kiến thức đạt được |
|---|---|
| Amazon S3 | Hiểu Block Public Access, SSE-KMS, versioning, presigned POST và điều kiện policy. |
| Amazon DynamoDB | Hiểu partition key, sort key, conditional update, Query và pagination token. |
| API Gateway và Lambda | Hiểu proxy integration, kiểm tra request và vai trò IAM riêng cho từng Lambda. |

### Công việc thực hiện

- Triển khai upload contract có giới hạn MIME type, kích thước, object key và mã hóa.
- Xác nhận chữ ký PDF, kích thước, metadata và SHA-256 trước khi chuyển trạng thái.
- Xây dựng API list, get và delete bằng compound key của owner và document ID; xóa cả S3 versions và delete markers.

## Anh Đức

### Kiến thức AWS

| Nội dung | Kiến thức đạt được |
|---|---|
| S3 presigned request | Hiểu trình duyệt upload trực tiếp mà không nhận AWS secret và backend vẫn kiểm soát policy. |
| DynamoDB access pattern | Hiểu thiết kế bảng bắt đầu từ truy vấn list/get/delete và phạm vi owner. |
| AWS SDK | Hiểu cách frontend nhận upload contract, gửi form tới S3 và gọi API quản lý tài liệu. |

### Công việc thực hiện

- Thiết kế luồng upload, danh sách, chi tiết, phân trang và xác nhận xóa trên giao diện.
- Bổ sung kiểm tra file phía client và trạng thái đang tải, thành công, lỗi an toàn.
- Xây dựng test case cho PDF thật, sai định dạng, quá giới hạn, key bị sửa và xóa lặp lại.

## Kết quả và bằng chứng

- PDF thật chuyển từ `PENDING_UPLOAD` sang `UPLOADED`; file giả, file quá lớn và key bị sửa đều bị chặn.
- S3 private, mã hóa, versioning và Block Public Access được kiểm chứng.
- API dùng DynamoDB `Query`, phân trang không lộ `LastEvaluatedKey`, thao tác lặp lại an toàn.
