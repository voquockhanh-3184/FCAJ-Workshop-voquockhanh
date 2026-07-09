---
title : "Tạo Cognito User Pool"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.4.4. </b> "
---

#### Khái niệm:
Một **Amazon Cognito User Pool** là một thư mục người dùng được quản lý hoàn toàn (fully managed user directory), chịu trách nhiệm xử lý việc đăng ký, đăng nhập và phân quyền người dùng cho các ứng dụng web và di động. Nó hoạt động như một nhà cung cấp danh tính OpenID Connect (OIDC) và phát hành các mã thông báo JWT chứa các thông tin xác thực (claims) của người dùng đã đăng nhập thành công.

#### Mục tiêu:
Tạo một **Amazon Cognito User Pool** để quản lý quy trình đăng ký, đăng nhập và phân quyền cho dự án Examora, đồng thời cấu hình để hệ thống tự động gửi email xác thực thông qua dịch vụ **Amazon SES**.

#### Các bước cấu hình thực hiện:

1. Tìm kiếm và chọn dịch vụ **Cognito** trong giao diện AWS Management Console.
- Tại menu thanh bên trái, chọn mục **User pools** -> Nhấn chọn **Create user pool**.

![Tạo User Pool](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.4-Cognito-SES/COGNITO4.1.png)

2. Cấu hình các thuộc tính của User Pool:
- Tại mục **Application type**, lựa chọn **Single-page application (SPA)**.
- Thiết lập tên cho User Pool (Ví dụ: `examora-user-pool`).
- Tại mục **Configure options**, tích chọn ô **Email**.
- Nhập đường dẫn Frontend Local URL của bạn (đường dẫn này sẽ được cập nhật lại sau khi phân phối thực tế qua S3 + CloudFront).
- Nhấn chọn **Create user directory** để khởi tạo thư mục người dùng.

![Cấu hình ứng dụng SPA](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.4-Cognito-SES/COGNITO4.2.png)

![Thông tin User Directory](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.4-Cognito-SES/COGNITO4.3.png)

3. Nhấp chọn vào User Pool vừa tạo để thu thập các biến môi trường cấu hình quan trọng sau đây:
- `AWS_REGION = ap-southeast-1`
- `COGNITO_USER_POOL_ID = <User Pool ID của bạn>`
- `COGNITO_APP_CLIENT_ID = <Client ID của bạn>`
- `COGNITO_ISSUER_URL = https://cognito-idp.ap-southeast-1.amazonaws.com/<User Pool ID>`

4. Cấu hình tính năng tự động gửi email xác thực khi người dùng đăng ký:
- Tại mục **Attribute verification and user account confirmation** -> Tích chọn **Allow Cognito to automatically send messages to verify and confirm** và chọn phương thức **Send email message, verify email address**.
- Cấu hình này cho phép Cognito tự động gửi các mã OTP để xác thực và kích hoạt tài khoản của người dùng ngay sau khi đăng ký thành công.

![Xác thực thuộc tính người dùng](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.4-Cognito-SES/COGNITO4.4.png)

5. Cập nhật lại biểu mẫu nội dung thông báo (Verification message template) để email xác thực phù hợp với nhận diện và phong cách thiết kế của dự án Examora.

![Biểu mẫu nội dung email](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.4-Cognito-SES/COGNITO4.5.png)