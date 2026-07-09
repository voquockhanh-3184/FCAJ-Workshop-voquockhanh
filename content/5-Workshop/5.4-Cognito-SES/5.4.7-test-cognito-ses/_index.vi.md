---
title : "Kiểm thử Cognito + SES"
date : 2024-01-01 
weight : 5
chapter : false
pre : " <b> 5.4.7. </b> "
---

#### Các bước kiểm thử:

1. Trong giao diện Cognito User Pool, điều hướng tới tab **App integration** -> Di chuyển xuống phần **App clients** -> Chọn App Client vừa khởi tạo.
2. Tại mục **Hosted UI**, bấm chọn **View login page** để mở trang đăng ký/đăng nhập mặc định của Cognito.

![View Login Page](/images/5-Workshop/5.4-Cognito-SES/TestCognitoSES4.1.png)

3. Tiến hành thử nghiệm đăng ký tài khoản mới:
- Điền các thông tin Email, Mật khẩu. 
- *Lưu ý:* Cần sử dụng các địa chỉ email đã được xác thực (verify) trước đó trong SES (do đang ở trạng thái SES Sandbox).
- Bấm **Sign up**.

![Hosted UI Sign up](/images/5-Workshop/5.4-Cognito-SES/TestCognitoSES4.2.png)

4. Một email chứa mã xác minh OTP sẽ được gửi từ Amazon SES đến hộp thư đăng ký của người dùng. Kiểm tra hộp thư -> Lấy mã OTP và nhập vào ô **Verification code** trên giao diện Cognito Hosted UI.

![Enter Verification Code](/images/5-Workshop/5.4-Cognito-SES/TestCognitoSES4.3.png)

5. Sau khi nhập đúng mã OTP và xác thực thành công, quay trở lại Cognito Console:
- Chọn tab **Users** trong User Pool của bạn.
- Kiểm tra danh sách người dùng. Nếu tài khoản mới đăng ký hiển thị trạng thái **Confirmed** ở cột **Confirmation status**, tức là quá trình tích hợp Cognito và SES đã hoạt động chính xác.

![User Confirmed Status](/images/5-Workshop/5.4-Cognito-SES/TestCognitoSES4.4.png)
