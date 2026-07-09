---
title : "Cấu hình S3 Upload Bucket và Presigned URL"
date : 2024-01-01 
weight : 7 
chapter : false
pre : " <b> 5.7. </b> "
---

#### Mục tiêu:
*   Tạo **S3 Upload Bucket** để lưu trữ ảnh, tài liệu và file Word trực tiếp từ người dùng mà không cần đi qua Lambda Backend API để xử lý/lưu file tĩnh, giúp giảm tải cho serverless backend.
*   Sử dụng cơ chế **Presigned URL** để Frontend tải file trực tiếp lên Amazon S3 một cách bảo mật.



#### Nội dung:
1. [Tạo S3 Upload Bucket và cấu hình CORS](5.7.1-create-s3-bucket/)
2. [Quy ước tiền tố đường dẫn (Prefix) tổ chức file](5.7.2-prefix-convention/)
3. [Cấp quyền truy cập S3 cho Lambda Backend API](5.7.3-grant-s3-permission-lambda/)
4. [Thiết kế Lambda Presigned URL Generator](5.7.4-design-presigned-url-generator/)
5. [Kiểm thử Presigned URL Endpoint và Upload file lên S3](5.7.5-test-presigned-url-upload/)
6. [Tạo thêm Lambda (Import Word Processor)](5.7.6-create-import-word-processor/)
