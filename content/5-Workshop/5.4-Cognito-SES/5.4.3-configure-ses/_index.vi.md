---
title : "Cấu hình Amazon SES cho Email của Cognito"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.4.3. </b> "
---

#### Các bước cấu hình thực hiện:

1. Đăng nhập vào AWS Management Console và đảm bảo rằng bạn đã chọn chính xác vùng (region): **Singapore (ap-southeast-1)**.
2. Tại thanh tìm kiếm của AWS, nhập **Amazon SES** -> Chọn **Amazon Simple Email Service** -> Tìm và chọn mục **Identities** nằm ở phần cấu hình trong menu bên trái.

![Amazon SES Identities](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.4-Cognito-SES/SES4.1.png)

3. Tạo danh tính email người gửi (sender email identity):
- Nhấn nút **Create identity**.

![Tạo Danh Tính](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.4-Cognito-SES/SES4.2.png)

- Tại phần **Identity details**, tích chọn mục **Email address** ở phần **Identity type**.
- Nhập địa chỉ email mà bạn muốn sử dụng làm địa chỉ gửi thư cho hệ thống Examora.
- Nhấn chọn **Create identity** ở góc dưới cùng.

![Chi Tiết Email](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.4-Cognito-SES/SES4.3.png)

- Truy cập vào hộp thư đến của địa chỉ email vừa đăng ký. Tìm và nhấp vào liên kết xác thực do AWS gửi đến để tiến hành xác nhận danh tính email.

![Xác Thực Email](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.4-Cognito-SES/SES4.4.png)

- Sau khi xác thực xong, trạng thái danh tính (identity status) trên AWS Console sẽ chuyển sang **Verified**. Điều này xác nhận địa chỉ email người gửi đã được kích hoạt thành công.

![Xác Thực SES Thành Công](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.4-Cognito-SES/SES4.5.png)

#### Kết luận:
*   Chúng ta đã cấu hình thành công dịch vụ **Amazon SES** tại vùng `ap-southeast-1` và xác thực địa chỉ email người gửi cho dự án Examora. Danh tính email này sẽ được đưa vào cấu hình của Cognito User Pool nhằm gửi các mã xác thực và mã khôi phục mật khẩu cho người dùng.
*   Theo mặc định, các tài khoản SES mới tạo sẽ nằm trong **môi trường thử nghiệm Sandbox**, nghĩa là chỉ có thể gửi email đến các địa chỉ hoặc tên miền đã được xác thực trước. Do đó, phục vụ cho việc kiểm thử, chúng ta phải tiến hành xác thực riêng lẻ các địa chỉ email kiểm thử được gán cho các tài khoản ADMIN, TEACHER và STUDENT. Để chuyển sang môi trường thực tế (production) sau này, bạn cần gửi yêu cầu **SES Production Access** nhằm gửi thư đến các người nhận chưa qua xác thực.