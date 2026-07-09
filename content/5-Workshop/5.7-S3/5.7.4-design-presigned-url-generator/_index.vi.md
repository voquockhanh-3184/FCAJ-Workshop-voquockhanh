---
title : "Thiết kế Lambda Presigned URL Generator"
date : 2024-01-01 
weight : 4
chapter : false
pre : " <b> 5.7.4. </b> "
---

#### Mục tiêu:
Thiết kế chức năng tạo presigned URL để frontend Examora có thể upload file trực tiếp lên S3 Upload Bucket, thay cho cơ chế upload file qua backend local `/public/uploads`.

#### Luồng hoạt động:
`Frontend → API Gateway → Lambda Backend API → tạo presigned URL → Frontend upload file trực tiếp lên S3`


*Lưu ý:*
Trong sơ đồ kiến trúc của Examora, Lambda Presigned URL Generator biểu diễn chức năng tạo presigned URL cho upload S3. Chức năng này được triển khai bên trong Lambda Backend API để tận dụng middleware xác thực JWT, kiểm tra role và logic nghiệp vụ hiện có.

---

#### Các bước thực hiện:

1. Thêm inline policy S3 Upload Bucket bằng JSON vào IAM execution role của Lambda Backend API:
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
         "Resource": "arn:aws:s3:::examora-s3-upload-bucket-505284748625-ap-southeast-1-an/*"
       }
     ]
   }
   ```

   ![Thêm inline policy JSON](/images/5-Workshop/5.7-S3/5.7.4-design-presigned-url-generator/LambdaURL2.png)

   * Đặt tên cho policy: `examora-backend-upload-bucket-policy-dev`.

   ![Đặt tên Policy](/images/5-Workshop/5.7-S3/5.7.4-design-presigned-url-generator/LambdaURL3.png)

2. Quay lại Function của Lambda Backend API, thêm cấu hình cho môi trường:

   ![Cấu hình Environment variables](/images/5-Workshop/5.7-S3/5.7.4-design-presigned-url-generator/LambdaURL4.png)

3. Cập nhật code Backend Lambda:
   * Trong thư mục Backend, cài thêm package `@aws-sdk/s3-request-presigner` để tạo signed URL cho S3:

   ![Cài đặt S3 Request Presigner](/images/5-Workshop/5.7-S3/5.7.4-design-presigned-url-generator/LambdaURL5.png)

   * Bổ sung thêm endpoint: `POST /api/uploads/presigned-url`. Endpoint này thực hiện:
     * Đọc JWT/user từ middleware protect.
     * Lấy `cognitoGroups` hoặc role của user.
     * Kiểm tra `uploadType`.
     * Sinh object key theo prefix quy ước.
     * Tạo presigned URL bằng `PutObjectCommand`.
     * Trả `uploadUrl` cho frontend.

4. Đóng gói lại source code Backend và upload lại lên Lambda `examora-backend-api-dev`.
