---
title : "Cấp quyền truy cập S3 cho Lambda Backend API"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.7.3. </b> "
---

Để Lambda Backend API có thể ký và tạo Presigned URL cho S3 Upload Bucket, chúng ta cần bổ sung thêm các quyền truy cập S3 tương ứng vào IAM execution role của Lambda và cấu hình biến môi trường.

#### Các bước thực hiện:

1. Tạo Inline Policy cho S3:
   * Truy cập dịch vụ **IAM** -> Chọn **Roles** -> Tìm và chọn IAM execution role của Lambda Backend API (ví dụ: `examora-lambda-backend-role`).
   * Tại tab **Permissions** -> Chọn **Add permissions** -> Chọn **Create inline policy**.

   ![Thêm Permissions Inline Policy](/images/5-Workshop/5.7-S3/5.7.3-grant-s3-permission-lambda/IAMpermissions1.png)

   * Chọn phương thức soạn thảo bằng **JSON** và dán đoạn policy dưới đây:

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "ExamoraUploadBucketObjectAccess",
         "Effect": "Allow",
         "Action": [
           "s3:PutObject",
           "s3:GetObject"
         ],
         "Resource": "arn:aws:s3:::<UPLOAD_BUCKET_NAME>/*"
       }
     ]
   }
   ```
   *(Thay `<UPLOAD_BUCKET_NAME>` bằng tên S3 bucket của bạn đã tạo ở bước 5.7.1)*.

   ![Soạn thảo Policy bằng JSON](/images/5-Workshop/5.7-S3/5.7.3-grant-s3-permission-lambda/IAMpermissions2.png)

   * Nhấn **Next**.
   * Đặt tên cho policy (ví dụ: `examora-backend-upload-bucket-policy-dev`).
   * Chọn **Create policy** để hoàn tất.

   ![Đặt tên Inline Policy](/images/5-Workshop/5.7-S3/5.7.3-grant-s3-permission-lambda/IAMpermissions3.png)

   ![Policy S3 đã được gắn thành công](/images/5-Workshop/5.7-S3/5.7.3-grant-s3-permission-lambda/IAMpermissions4.png)

2. Khai báo cấu hình S3 Bucket làm biến môi trường cho Lambda:
   * Quay lại dịch vụ **Lambda** -> Chọn hàm `examora-backend-api` -> Chọn tab **Configuration** (Cấu hình) -> Chọn **Environment variables** -> Bấm **Edit**.
   * Thêm các biến môi trường sau:
     * `UPLOAD_BUCKET_NAME` = `<Tên S3 Bucket đã tạo>`
     * `UPLOAD_BUCKET_REGION` = `ap-southeast-1`
   * Bấm **Save** để lưu lại.

   ![Cấu hình biến môi trường S3](/images/5-Workshop/5.7-S3/5.7.3-grant-s3-permission-lambda/EnvBucket1.png)
