---
title : "Cấu hình Cognito User Pool + SES cho Examora"
date : 2024-01-01 
weight : 4 
chapter : false
pre : " <b> 5.4. </b> "
---

Trong bước này, chúng ta sẽ cấu hình **Amazon Cognito User Pool** kết hợp với **Amazon SES** để xử lý các chức năng xác thực và phân quyền người dùng cho dự án **Examora - Online Exam Platform **.

#### 5.4.1. Mục tiêu
Hệ thống xác thực sẽ quản lý các chức năng chính bao gồm:
*   Đăng ký và đăng nhập tài khoản bằng Email/Mật khẩu.
*   Tự động gửi mã xác minh (verification code) qua email khi đăng ký.
*   Quên mật khẩu và thay đổi mật khẩu (forgot/reset password).
*   Phát hành mã xác thực JWT (JSON Web Tokens) sau khi đăng nhập thành công.
*   Phân nhóm người dùng (Cognito Groups) để phân quyền truy cập: **ADMIN**, **TEACHER**, **STUDENT**.

#### 5.4.2. Phạm vi cấu hình
Các tài nguyên và cấu hình cần thiết lập bao gồm:
1.  **Amazon SES Verified Identity**: Xác minh danh tính email gửi.
2.  **Cognito User Pool**: Thiết lập nhóm người dùng.
3.  **Cognito App Client**: Cấu hình ứng dụng khách.
4.  **Cognito Groups**: Khởi tạo 3 nhóm ADMIN, TEACHER, STUDENT.
5.  **Cấu hình SES trong Cognito**: Tích hợp SES làm Email Provider.
6.  **Kiểm thử**: Đăng ký, nhập mã OTP và xác thực trạng thái Confirm.

#### Nội dung

1. [Cấu hình Amazon SES cho email gửi từ Cognito](5.4.3-configure-ses/)
2. [Tạo Cognito User Pool cho Examora](5.4.4-create-user-pool/)
3. [Tạo Cognito Groups cho Examora](5.4.5-create-cognito-groups/)
4. [Cấu hình email gửi bằng SES](5.4.6-configure-email-ses/)
5. [Kiểm thử Cognito + SES gửi email trên Console](5.4.7-test-cognito-ses/)
