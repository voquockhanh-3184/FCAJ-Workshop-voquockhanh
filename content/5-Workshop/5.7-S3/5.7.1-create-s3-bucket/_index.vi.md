---
title : "Tạo S3 Upload Bucket và cấu hình CORS"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.7.1. </b> "
---

#### Các bước thực hiện:

1. Tạo S3 Bucket:
   * Truy cập vào bảng điều khiển **Amazon S3** -> Chọn **Buckets** ở menu trái -> Chọn **Create bucket**.
   * Cấu hình thông tin cơ bản:
     * **Bucket name**: Đặt tên duy nhất trên toàn cầu cho bucket của bạn (ví dụ: `examora-s3-upload-bucket`).
     * **AWS Region**: Chọn `ap-southeast-1` (Singapore).
     * Các cấu hình khác giữ nguyên mặc định -> Chọn **Create bucket** ở cuối trang.

   ![Tạo S3 Bucket](/images/5-Workshop/5.7-S3/5.7.1-create-s3-bucket/S3UpLoad6.2.png)

2. Cấu hình CORS Policy cho bucket vừa tạo:
   * Sau khi bucket được tạo thành công, bấm mở tên bucket -> Chọn tab **Permissions** (Quyền truy cập).
   * Cuộn xuống mục **Cross-origin resource sharing (CORS)** -> Chọn **Edit**.

   ![Cấu hình CORS S3](/images/5-Workshop/5.7-S3/5.7.1-create-s3-bucket/S3UpLoad6.3.png)

   * Điền nội dung cấu hình JSON dưới đây:

   ```json
   [
     {
       "AllowedHeaders": ["*"],
       "AllowedMethods": ["PUT", "GET", "HEAD"],
       "AllowedOrigins": ["http://localhost:5173"],
       "ExposeHeaders": ["ETag"],
       "MaxAgeSeconds": 3000
     }
   ]
   ```

   * Nhấn **Save changes** để hoàn tất.

   ![Lưu CORS S3 thành công](/images/5-Workshop/5.7-S3/5.7.1-create-s3-bucket/S3UpLoad6.4.png)

#### Chú thích:
Cấu hình CORS Policy cho S3 Upload Bucket nhằm cho phép ứng dụng frontend React (chạy ở localhost `http://localhost:5173` hoặc domain production) có quyền upload file tĩnh trực tiếp lên S3 bằng Presigned URL mà không bị chặn bởi cơ chế bảo mật Same-Origin Policy của trình duyệt.
