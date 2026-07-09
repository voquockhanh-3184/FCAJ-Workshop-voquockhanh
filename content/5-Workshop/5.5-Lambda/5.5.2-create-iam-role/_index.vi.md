---
title : "Tạo IAM Role cho Lambda Backend API"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.5.2. </b> "
---

AWS Lambda function cần một **execution role** (vai trò thực thi) để truy cập các dịch vụ AWS khác. Chúng ta sẽ tiến hành tạo execution role riêng cho Lambda Backend API theo nguyên tắc đặc quyền tối thiểu (least privilege).

#### Các bước thực hiện:

1. Truy cập trang quản lý [Roles](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles) trong dịch vụ IAM, sau đó bấm chọn **Create role**.

2. Cấu hình thực thể tin cậy (Trusted entity):
   * **Trusted entity type**: Chọn **AWS service**.
   * **Service or use case**: Chọn **Lambda**.
   * Bấm **Next**.

   ![Chọn Trusted Entity](/images/5-Workshop/5.5-Lambda/5.5.2-create-iam-role/LambdaBE5.2.png)

3. Gán các quyền cơ bản để ghi log và theo dõi trace: tại phần **Permissions policies**, tìm kiếm và tích chọn:
   * **AWSLambdaBasicExecutionRole**: Quyền cơ bản cho phép Lambda ghi nhật ký hoạt động vào Amazon CloudWatch Logs.
   * **AWSXRayDaemonWriteAccess**: Quyền cho phép Lambda gửi thông tin trace sang dịch vụ AWS X-Ray.

   ![Chọn Permission Policies](/images/5-Workshop/5.5-Lambda/5.5.2-create-iam-role/LambdaBE5.3.png)

4. Đặt tên và tạo Role:
   * **Role name**: Nhập tên dễ nhớ (ví dụ: `examora-lambda-backend-role`).
   * Kiểm tra lại cấu hình và chọn **Create role**.

   ![Đặt tên Role](/images/5-Workshop/5.5-Lambda/5.5.2-create-iam-role/LambdaBE5.4.png)

5. Gán quyền đọc Secrets Manager cho Lambda (để kết nối tới MongoDB Atlas):
   * Mở role vừa tạo -> Tại tab **Permissions** -> Bấm **Add permissions** -> Chọn **Create inline policy**.
   * Chọn tab **JSON** và nhập nội dung chính sách sau (thay thế `<ACCOUNT_ID>` bằng ID tài khoản AWS của bạn):

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "ReadExamoraMongoDBSecret",
         "Effect": "Allow",
         "Action": [
           "secretsmanager:GetSecretValue"
         ],
         "Resource": "arn:aws:secretsmanager:ap-southeast-1:<ACCOUNT_ID>:secret:/examora/dev/mongodb-*"
       }
     ]
   }
   ```
   * *Lưu ý*: Trong đó `/examora/dev/mongodb` là secret đã tạo ở AWS Secrets Manager chứa các thông tin `MONGO_URI` và `MONGO_DB_NAME`.
   * Đặt tên cho policy (ví dụ: `examora-lambda-secrets-policy`) -> Bấm **Create policy**.

   ![Gán Inline Policy](/images/5-Workshop/5.5-Lambda/5.5.2-create-iam-role/LambdaBE5.5.png)

Như vậy, chúng ta đã tạo xong IAM Execution Role cho Lambda Backend API.
