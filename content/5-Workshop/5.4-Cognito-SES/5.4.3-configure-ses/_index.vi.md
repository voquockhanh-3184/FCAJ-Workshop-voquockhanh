---
title : "Cấu hình Amazon SES cho email gửi từ Cognito"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.4.3. </b> "
---

#### Các bước cấu hình:

1. Đăng nhập vào AWS Console, chọn đúng Region hoạt động: **Singapore (ap-southeast-1)**.
2. Trên thanh tìm kiếm, gõ **Amazon SES** -> Chọn **Amazon Simple Email Service** -> Tìm và chọn mục **Identities** ở danh mục cấu hình (Configuration) bên trái.

![Amazon SES Identities](/images/5-Workshop/5.4-Cognito-SES/SES4.1.png)

3. Tiến hành tạo địa chỉ email đại diện để gửi:
- Nhấn chọn nút **Create identity**.

![Create Identity](/images/5-Workshop/5.4-Cognito-SES/SES4.2.png)

- Tại phần **Identity details**, tích chọn **Email address** ở mục **Identity type**.
- Điền địa chỉ email của bạn muốn sử dụng làm địa chỉ gửi (sender) của Examora.
- Nhấn **Create identity** ở phía dưới để khởi tạo.

![Email Details](/images/5-Workshop/5.4-Cognito-SES/SES4.3.png)

- Mở hộp thư của email bạn vừa đăng ký, tìm và bấm vào đường dẫn (verification link) được gửi về từ AWS để xác thực địa chỉ email.

![Email Verification Verification](/images/5-Workshop/5.4-Cognito-SES/SES4.4.png)

- Sau khi xác nhận xong, trạng thái của email trên console sẽ hiển thị **Verified**. Như vậy là chúng ta đã xác minh địa chỉ email gửi thành công.

![SES Identity Verified](/images/5-Workshop/5.4-Cognito-SES/SES4.5.png)

#### Kết luận:
*   Chúng ta đã cấu hình thành công **Amazon SES** tại Region `ap-southeast-1` và xác minh địa chỉ email gửi (sender email identity) cho Examora. Email này sẽ được sử dụng trong cấu hình Cognito User Pool để gửi mã xác minh đăng ký (verification code) và mã khôi phục mật khẩu (reset password code) cho người dùng.
*   Do tài khoản SES khi mới tạo mặc định ở trạng thái Sandbox, hệ thống chỉ gửi được email đến các địa chỉ email hoặc tên miền đã được xác minh trước đó trong SES. Vì vậy, trong phạm vi thử nghiệm, chúng ta cần verify thêm các email test dùng cho các tài khoản ADMIN, TEACHER và STUDENT. Khi triển khai dự án thực tế (Production), bạn cần gửi yêu cầu **SES Production Access** để có thể gửi email đến bất kỳ người dùng nào.
