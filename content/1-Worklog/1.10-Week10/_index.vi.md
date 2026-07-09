---
title: "Worklog Tuần 10"
date: 2026-06-26
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---


### Mục tiêu tuần 10:

* Chuyển đổi luồng tải tập tin (upload file) sang S3 Upload Bucket bằng phương thức Presigned URL.
* Tách biệt tính năng import tài liệu Word thành một AWS Lambda riêng biệt để xử lý bất đồng bộ (asynchronous).

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Công cụ / Nền tảng |
| --- | --- | --- | --- | --- |
| 2 | - **Thiết kế Quy ước S3 Prefix:** <br>&emsp; + Đề xuất và thống nhất quy ước đặt tên prefix trong S3 Upload Bucket <br>&emsp; + Phân chia các phân vùng lưu trữ cho avatar, ảnh lớp học, ảnh đề thi, ảnh câu hỏi và tệp tin import Word | 22/06/2026 | 22/06/2026 | [cloudjourney.awsstudygroup.com](https://000057.awsstudygroup.com/) |
| 3 | - **Xây dựng Logic Tạo Presigned URL:** <br>&emsp; + Triển khai mã nguồn sinh Presigned URL tại API Backend chính <br>&emsp; + Cấu hình các điều kiện ràng buộc về định dạng và dung lượng file trước khi cấp quyền upload | 23/06/2026 | 23/06/2026 | AWS SDK / Node.js |
| 4 | - **Phát triển Lambda Xử lý Bất đồng bộ:** <br>&emsp; + Xây dựng mã nguồn cho hàm Lambda độc lập chuyên phụ trách parse file `.docx` <br>&emsp; + Tích hợp thư viện giải mã cấu trúc văn bản hoạt động tối ưu trong môi trường serverless | 24/06/2026 | 24/06/2026 | AWS Lambda / S3 Trigger |
| 5 | - **Kiểm thử Upload và Xác thực Phân vùng:** <br>&emsp; + Thực hiện kiểm thử upload tập tin `.docx` thông qua Presigned URL đã sinh <br>&emsp; + Kiểm tra và đảm bảo object xuất hiện chính xác dưới phân vùng định sẵn `imports/word/raw/` trên S3 | 25/06/2026 | 25/06/2026 | [Amazon S3 User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/) |
| 6 | - **Kiểm thử Luồng Import Toàn diện (E2E Async):** <br>&emsp; + Kiểm tra cơ chế trigger tự động từ S3 Event kích hoạt sang hàm Lambda xử lý <br>&emsp; + Xác thực dữ liệu câu hỏi sau khi bóc tách được lưu trữ thành công và đúng định dạng vào MongoDB | 26/06/2026 | 26/06/2026 | MongoDB Atlas / CloudWatch |

### Kết quả đạt được tuần 10:

* Kích thái thành công cơ chế Presigned URL hoạt động ổn định cho các luồng upload dữ liệu chính, giúp tối ưu hóa hiệu năng ứng dụng và giảm tải cho server backend.
* Chuẩn hóa cấu trúc lưu trữ trên Cloud, đảm bảo toàn bộ tệp tin được phân loại và lưu trữ một cách hệ thống đúng theo tiền tố (prefix) S3 quy định.
* Tách biệt và phát triển thành công hàm Lambda Import Word hoạt động bất đồng bộ, có khả năng tự động xử lý và bóc tách các file văn bản dạng `.docx` độc lập.
* Hoàn thiện quy trình tích hợp khép kín, tự động trích xuất cấu trúc đề thi, câu hỏi từ tài liệu và lưu trữ chính xác vào cơ sở dữ liệu MongoDB.