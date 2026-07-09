---
title : "Tạo Cognito User Pool cho Examora"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.4.4. </b> "
---

#### Khái niệm:
**Amazon Cognito User Pool** là một danh bạ người dùng (user directory) được quản lý hoàn toàn nhằm xử lý xác thực (authentication) và phân quyền (authorization) cho các ứng dụng web và di động. User Pool hoạt động như một OpenID Connect (OIDC) identity provider và phát hành các JWT tokens chứa thông tin xác thực của người dùng.

#### Mục tiêu:
Tạo **Amazon Cognito User Pool** để xử lý đăng ký, đăng nhập và phân quyền cho Examora, đồng thời thiết lập tự động gửi email xác minh thông qua **Amazon SES**.

#### Các bước thực hiện:

1. Tìm và chọn dịch vụ **Cognito** trên AWS Console.
- Tại menu bên trái, chọn **User pools** -> Bấm **Create user pool**.

![Create User Pool](/images/5-Workshop/5.4-Cognito-SES/COGNITO4.1.png)

2. Cấu hình các thông số cho User Pool:
- Tại mục **Application type**, chọn **Single-page application (SPA)**.
- Đặt tên cho User Pool (ví dụ: `examora-user-pool`).
- Tại phần **Configure options**, tích chọn **Email**.
- Điền URL của Frontend Local vào mục tương ứng (đường dẫn này sẽ được cập nhật lại sau khi deploy lên S3 + CloudFront).
- Nhấn chọn **Create user directory** để tạo.

![Configure SPA](/images/5-Workshop/5.4-Cognito-SES/COGNITO4.2.png)

![User Directory Info](/images/5-Workshop/5.4-Cognito-SES/COGNITO4.3.png)

3. Nhấp chọn User Pool vừa tạo để lấy các thông số môi trường quan trọng sau:
- `AWS_REGION = ap-southeast-1`
- `COGNITO_USER_POOL_ID = <User Pool ID của bạn>`
- `COGNITO_APP_CLIENT_ID = <Client ID của bạn>`
- `COGNITO_ISSUER_URL = https://cognito-idp.ap-southeast-1.amazonaws.com/<User Pool ID>`

4. Cấu hình tự động gửi email xác minh tài khoản khi người dùng đăng ký:
- Ở phần **Attribute verification and user account confirmation** -> Chọn **Allow Cognito to automatically send messages to verify and confirm** và **Send email message, verify email address**.
- Cấu hình này cho phép Cognito tự động gửi mã OTP xác nhận tài khoản tới địa chỉ email đăng ký của người dùng.

![Attribute Verification](/images/5-Workshop/5.4-Cognito-SES/COGNITO4.4.png)

5. Tinh chỉnh tiêu đề và nội dung email xác minh (Verification message template) cho phù hợp với thương hiệu dự án Examora.

![Message Template](/images/5-Workshop/5.4-Cognito-SES/COGNITO4.5.png)
