---
title: "Bản đề xuất"
date: 2026-07-29
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

## Nền tảng thông tin tài liệu tài chính serverless trên AWS

### 1. Tóm tắt dự án

FinSight AI hỗ trợ người dùng rà soát báo cáo tài chính công khai hoặc tổng hợp. Người dùng đã xác thực tải một tệp PDF lên vùng riêng tư; hệ thống trích xuất văn bản nhúng theo trang và AI trả kết quả có cấu trúc gồm chỉ số tài chính, xu hướng, rủi ro, bất thường, giới hạn và trích dẫn trang.

AWS cung cấp xác thực, phân phối frontend, API được bảo vệ, lưu trữ riêng tư, xử lý bất đồng bộ, bảo mật và giám sát. Google Gemini gemini-2.5-flash là provider development bên ngoài đang hoạt động. Amazon Bedrock vẫn là mặc định trong source/template, Groq đã được triển khai nhưng không hoạt động và không có fallback tự động.

PDF gốc vẫn nằm trong vùng lưu trữ AWS riêng tư. Chỉ văn bản trích xuất đáng tin cậy và metadata cần thiết được gửi đến Gemini. Kết quả hỗ trợ con người rà soát và không phải tư vấn đầu tư.

**Quy mô nhóm:** 2 thành viên

### 2. Vấn đề cần giải quyết

#### Vấn đề là gì?

Báo cáo tài chính thường dài và chứa thông tin trên nhiều trang. Rà soát thủ công tốn thời gian, rủi ro quan trọng có thể bị bỏ sót và bản tóm tắt không có trích dẫn trang rất khó xác minh. Trích xuất PDF và phân tích AI cũng có thể lỗi, vượt giới hạn kích thước hoặc kéo dài hơn một yêu cầu đồng bộ thông thường.

#### Giải pháp

FinSight AI cung cấp tải lên riêng tư có xác thực, xử lý bất đồng bộ, trích xuất văn bản nhúng, phân tích AI có cấu trúc và trích dẫn theo trang. Chủ sở hữu được máy chủ suy ra, storage luôn riêng tư và phản hồi AI sai hoặc chưa hoàn chỉnh bị từ chối.

#### Lợi ích

- Giảm thời gian tìm thông tin tài chính quan trọng.
- Giúp kiểm tra nhận định dễ hơn bằng trích dẫn trang.
- Minh họa kiến trúc AWS serverless, hướng sự kiện và an toàn.
- Cung cấp trạng thái xử lý rõ, retry có kiểm soát, giám sát và xóa an toàn.

### 3. Kiến trúc giải pháp

FinSight AI sử dụng kiến trúc AWS serverless để xử lý tài liệu tài chính an toàn. React/Vite frontend được CloudFront phân phối từ S3 origin riêng tư. Người dùng đã xác nhận nhận thông tin xác thực tạm từ Cognito và ký protected API request bằng SigV4. Sau khi PDF riêng tư được xác minh và tải lên, DynamoDB Streams, SQS, Lambda và Step Functions điều phối trích xuất văn bản nhúng cùng phân tích có cấu trúc. Kết quả đã kiểm tra vẫn ở trạng thái riêng tư và chỉ được trả cho chủ sở hữu tài liệu.

![Sơ đồ kiến trúc giải pháp FinSight AI](/images/2-Proposal/finsight-ai-architecture.svg?v=3ec0ffd1)

#### Các dịch vụ AWS được sử dụng

- **Amazon CloudFront:** Phân phối React/Vite frontend qua HTTPS từ S3 origin riêng tư.
- **Amazon Cognito:** Xử lý xác thực email đã xác nhận và cấp thông tin xác thực AWS tạm.
- **Amazon API Gateway:** Cung cấp REST API được bảo vệ bằng AWS_IAM.
- **AWS Lambda:** Triển khai API tài liệu, dispatch sự kiện, trích xuất, phân tích, retry và xóa.
- **Amazon S3:** Lưu riêng tư frontend asset, PDF gốc, extraction artifact và kết quả đã xác thực.
- **Amazon DynamoDB:** Lưu metadata và lifecycle state theo chủ sở hữu; Streams kích hoạt xử lý.
- **Amazon SQS:** Đệm processing message và cách ly lỗi đã hết lượt thử trong DLQ.
- **AWS Step Functions:** Điều phối Standard workflow trích xuất và phân tích.
- **Amazon CloudWatch:** Cung cấp log có cấu trúc, embedded metrics, 10 alarm và khả năng quan sát execution.
- **AWS Secrets Manager:** Bảo vệ thông tin xác thực của provider bên ngoài được chọn.

#### Thiết kế thành phần

- **Giao diện web:** React/Vite hỗ trợ đăng ký, đăng nhập, tải PDF, tiến độ, kết quả, trích dẫn, retry và xóa.
- **Xác thực:** Cognito User Pool và Identity Pool cấp thông tin xác thực tạm; trình duyệt ký API request bằng SigV4.
- **Quản lý tài liệu:** Backend suy ra chủ sở hữu, kiểm tra PDF metadata và SHA-256, rồi lưu tệp trong S3 riêng tư có versioning.
- **Xử lý bất đồng bộ:** DynamoDB Streams và SQS tách xác nhận tải lên khỏi Step Functions workflow idempotent.
- **Trích xuất văn bản:** Lambda trích xuất văn bản nhúng theo trang và ghi tín hiệu chất lượng; hệ thống phát hiện nhu cầu OCR nhưng không thực thi OCR.
- **Phân tích AI:** Cấu hình triển khai đáng tin cậy chọn Gemini gemini-2.5-flash; Bedrock vẫn là mặc định trong source/template và Groq không hoạt động.
- **Kết quả và bảo mật:** Schema cùng trích dẫn trang được kiểm tra cục bộ, kết quả luôn riêng tư và truy cập chéo trả phản hồi không tìm thấy an toàn.
- **Khả năng quan sát:** CloudWatch giám sát log, metrics, alarm, queue, lỗi và trạng thái workflow mà không lưu toàn bộ văn bản tài liệu trong log.

### 4. Triển khai kỹ thuật

#### Các giai đoạn triển khai

1. Xác định phạm vi dự án, kiến trúc AWS, kiểm soát IAM, kế hoạch chi phí và nền tảng AWS SAM.
2. Triển khai tải PDF riêng tư, metadata theo chủ sở hữu, API tài liệu, idempotency và xóa an toàn.
3. Bổ sung DynamoDB Streams, SQS/DLQ, Step Functions, trích xuất văn bản nhúng và phát hiện chất lượng.
4. Bổ sung Cognito, browser SigV4, React frontend, phân tích AI có cấu trúc, kiểm tra trích dẫn, tích hợp Gemini, giám sát, kiểm thử và tài liệu release.

#### Yêu cầu kỹ thuật

- React, Vite, TypeScript, Python 3.12, AWS SAM và CloudFormation.
- Các managed serverless service AWS được liệt kê trong kiến trúc.
- Tệp PDF có văn bản nhúng.
- Báo cáo công khai, tổng hợp hoặc không nhạy cảm đã được phê duyệt cho xử lý development bằng Gemini.

OCR, RAG, cơ sở dữ liệu vector, khuyến nghị đầu tư, giao dịch tự động, SLA production và chứng nhận pháp lý nằm ngoài phạm vi hiện tại.

### 5. Tiến độ và cột mốc

- **Tuần 1 — 22/06–28/06:** xác định dự án, nền tảng AWS và kiến trúc.
- **Tuần 2 — 29/06–05/07:** tải lên an toàn và quản lý tài liệu.
- **Tuần 3 — 06/07–12/07:** xử lý bất đồng bộ và trích xuất PDF.
- **Tuần 4 — 13/07–19/07:** workflow, bảo mật, giám sát, chi phí và dọn dẹp.
- **Tuần 5 — 20/07–26/07:** Cognito, frontend, provider abstraction và phân tích có cấu trúc.
- **Tuần 6 — 27/07–02/08:** tích hợp Gemini, phục hồi lỗi và kiểm tra ứng dụng cuối.
- **Tuần 7 — 03/08–09/08:** báo cáo song ngữ, sơ đồ kiến trúc, ảnh chụp và review.
- **Tuần 8 — 10/08–15/08:** kiểm tra workshop, demo, rà soát quyền riêng tư, xuất bản và nộp bài.

### 6. Ước tính ngân sách

Ước tính sử dụng kiến trúc hiện tại tại Asia Pacific (Singapore) và kịch bản development quy mô nhỏ:

- 2 người dùng hoạt động;
- 100 tài liệu PDF mỗi tháng, khoảng 1 MiB mỗi tệp;
- 500 protected API request;
- dưới 1.000 Lambda invocation và 300 GB-giây;
- dưới 5.000 thao tác DynamoDB nhỏ;
- 100 workflow với dưới 1.000 Step Functions state transition;
- dưới 250 MiB dữ liệu S3 và các phiên bản;
- dưới 1 GiB log và dữ liệu truyền qua CloudFront; và
- 100 lần phân tích Gemini.

Mức giá được đối chiếu ngày 29/07/2026 bằng [AWS Pricing Calculator](https://calculator.aws/) và trang [Gemini API pricing](https://ai.google.dev/gemini-api/docs/pricing) chính thức.

#### Chi phí hạ tầng ước tính mỗi tháng

- **Amazon API Gateway:** 0,01 USD cho khoảng 500 REST request.
- **AWS Lambda:** 0,01 USD cho dưới 1.000 request và 300 GB-giây.
- **Amazon S3:** 0,02 USD cho dưới 0,25 GiB, các phiên bản và lượng request thấp.
- **Amazon DynamoDB:** 0,01 USD cho dưới 5.000 thao tác on-demand.
- **Amazon SQS:** 0,01 USD cho dưới 2.000 queue request.
- **AWS Step Functions:** 0,03 USD cho dưới 1.000 Standard state transition trước khi áp dụng free tier nếu đủ điều kiện.
- **Amazon CloudWatch:** dự phòng thận trọng 2,00 USD cho dưới 1 GiB log, embedded metrics và 10 standard alarm.
- **Amazon CloudFront:** 0,10 USD cho dưới 10.000 request và dưới 1 GiB dữ liệu truyền.
- **Amazon Cognito:** dự kiến 0,00 USD cho 2 monthly active user trong hạn mức áp dụng.
- **AWS Secrets Manager:** 0,40 USD cho một Gemini secret đang hoạt động và lượng API call thấp.
- **AWS CloudFormation:** không có phí dịch vụ bổ sung.

**Tổng AWS ước tính: 2,59 USD/tháng, tương đương 31,08 USD/12 tháng trước tín dụng và thuế.**

#### Chi phí AI bên ngoài

Kịch bản paid tier sử dụng kết quả tài liệu dài đã xác minh gồm 67.723 input token và 609 output token cho mỗi lần phân tích. Với 100 lần phân tích bằng Gemini gemini-2.5-flash:

- input: 6,7723 triệu token × 0,30 USD = 2,03 USD;
- output: 0,0609 triệu token × 2,50 USD = 0,15 USD; và
- **tổng Gemini ước tính: 2,18 USD/tháng, tương đương 26,21 USD/12 tháng.**

Gemini Free Tier có thể giảm khoản này về 0 USD khi còn đủ điều kiện, nhưng quota miễn phí và chính sách giá không được bảo đảm.

#### Tổng ngân sách dự kiến

**Tổng kết hợp ước tính: 4,77 USD/tháng, tương đương 57,29 USD/12 tháng.**

Chương trình học AWS cung cấp 200 USD tín dụng khuyến mại. Với kịch bản này, phần chi phí AWS nằm trong giới hạn đó, nhưng tín dụng AWS không thanh toán chi phí Gemini bên ngoài. Điều kiện áp dụng, ngày hết hạn tín dụng, thuế, mức sử dụng thực tế và giá tương lai phải được kiểm tra riêng. Dự án không lên kế hoạch mua phần cứng chuyên dụng.

### 7. Đánh giá rủi ro

#### Rủi ro chính

- Bedrock inference vẫn bị chặn bởi quota cấp tài khoản.
- Văn bản trích xuất rời AWS khi Gemini hoạt động.
- Đầu ra AI có thể không chính xác, sai định dạng, chưa hoàn chỉnh hoặc trích dẫn sai.
- Provider rate limit, gián đoạn và giới hạn đầu vào có thể làm ngắt phân tích.
- PDF quét cần OCR nhưng OCR chưa được triển khai.
- Truy cập trái phép, lộ bí mật, sự kiện trùng, workflow lỗi, chi phí ngoài dự kiến và chậm tiến độ vẫn có thể xảy ra.

#### Biện pháp giảm thiểu

FinSight AI dùng private storage, xác thực email đã xác nhận, thông tin xác thực tạm, chủ sở hữu do máy chủ suy ra, kiểm tra schema và trích dẫn, giới hạn máy chủ 1.000.000 ký tự, retry có kiểm soát, DLQ, CloudWatch alarm, Secrets Manager, log an toàn về quyền riêng tư và dữ liệu development công khai hoặc tổng hợp. Không rủi ro nào được xem là đã loại bỏ hoàn toàn.

### 8. Kết quả mong đợi

- Workflow an toàn từ xác thực người dùng và tải PDF riêng tư đến phân tích có cấu trúc và xóa an toàn.
- Thông tin tài chính có trích dẫn trang và nguồn gốc provider/model.
- Serverless infrastructure, giám sát, kiểm thử, kiểm soát chi phí và dọn dẹp có thể lặp lại.
- Báo cáo và workshop FCAJ song ngữ để trình diễn workflow development đã xác minh.
- Tài liệu học AWS thực tế, đồng thời thể hiện rõ yêu cầu con người rà soát và giới hạn hệ thống hiện tại.
