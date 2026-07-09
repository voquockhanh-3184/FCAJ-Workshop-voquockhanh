---
title : "Cấu hình email gửi bằng SES"
date : 2024-01-01 
weight : 4
chapter : false
pre : " <b> 5.4.6. </b> "
---

#### Khái niệm:
Theo mặc định, Amazon Cognito sẽ tự động gửi email cho người dùng thông qua máy chủ gửi mail mặc định của chính nó. Tuy nhiên, tính năng mặc định này bị giới hạn về số lượng gửi hàng ngày và độ tin cậy. 

Để tối ưu, Cognito cho phép tích hợp trực tiếp với **Amazon SES** để gửi email từ một địa chỉ email người gửi đã được xác thực (SES identity). Cấu hình này giúp tăng cường giới hạn gửi thư và độ tin cậy trong giao tiếp với người dùng.

#### Các bước thực hiện:

1. Chọn User Pool của bạn -> Nhấp chọn tab **Messaging**.
- Tìm tới mục **Email** -> Click chọn **Edit**.

![Edit Email Configuration](/images/5-Workshop/5.4-Cognito-SES/SES4.6.png)

2. Cấu hình SES làm nhà cung cấp email:
- Tại mục **Email provider**, chọn **Send email with Amazon SES (recommended)**.
- Tại mục **SES Identity**, chọn địa chỉ email mà bạn đã thực hiện xác minh ở bước [Cấu hình SES](../5.4.3-configure-ses) trước đó.
- Cấu hình các thông số gửi thư (Sender name, Reply-to email address nếu có).
- Nhấp chọn **Save changes** để lưu cấu hình.

![Save Changes](/images/5-Workshop/5.4-Cognito-SES/SES4.7.png)
