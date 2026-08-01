---
title: "Tuần 2"
date: 2026-06-29
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

**Thời gian:** 29/06/2026 – 05/07/2026

## Mục tiêu Tuần 2

- Triển khai upload PDF an toàn bằng presigned POST.
- Thiết kế metadata và vòng đời tài liệu trong DynamoDB.
- Xây dựng API list, get và delete theo owner.
- Bảo đảm thao tác lặp lại và xóa version an toàn.

## Nội dung học tập và công việc triển khai

| Thời gian | Nội dung học tập | Công việc áp dụng vào FinSight AI |
|---|---|---|
| Đầu tuần | Học S3 Block Public Access, SSE-KMS và versioning. | Tạo bucket private, mã hóa, có versioning và không cho public object. |
| Đầu tuần | Nghiên cứu presigned POST policy conditions. | Ràng buộc MIME type, kích thước, object key và header mã hóa trong upload contract. |
| Giữa tuần | Học DynamoDB partition key, sort key và conditional write. | Lưu metadata theo owner/document ID và kiểm soát chuyển trạng thái. |
| Giữa tuần | Tìm hiểu Query, pagination và opaque token. | Xây dựng API list không dùng Scan và không lộ LastEvaluatedKey. |
| Cuối tuần | Học S3 object versions, delete markers và idempotency. | Xóa toàn bộ versions/markers và hoàn tất tombstone DELETED an toàn khi retry. |

## Kết quả đạt được trong Tuần 2

- PDF thật chuyển từ PENDING_UPLOAD sang UPLOADED; file giả, quá lớn và key bị sửa bị chặn.
- S3 private, mã hóa, versioning và Block Public Access được kiểm chứng.
- API list/get/delete dùng owner-scoped compound key và pagination an toàn.
- Delete phục hồi được khi Lambda dừng giữa S3 cleanup và DynamoDB tombstone.
