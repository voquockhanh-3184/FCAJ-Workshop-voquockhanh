---
title: "Worklog Tuần 9"
date: 2026-06-19
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---


### Mục tiêu tuần 9:

* Triển khai hệ thống xác thực người dùng bằng Amazon Cognito và Amazon SES.
* Đưa mã nguồn Express backend hiện tại lên AWS Lambda dưới dạng Serverless.
* Bảo mật các endpoint và bảo vệ API bằng API Gateway JWT Authorizer.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Công cụ / Nền tảng |
| --- | --- | --- | --- | --- |
| 2 | - **Tối ưu hóa Cơ sở dữ liệu:** <br>&emsp; + Kiểm tra và xác thực cấu hình schema trong MongoDB Compass <br>&emsp; + Tạo `unique sparse index` cho trường `cognitoSub` trong collection `nguoidungs` | 15/06/2026 | 15/06/2026 | [MongoDB Compass](https://www.mongodb.com/docs/compass/) |
| 3 | - **Chuyển dịch Backend lên Lambda:** <br>&emsp; + Đóng gói ứng dụng Express.js thành một Lambda handler bằng thư viện serverless-express <br>&emsp; + Tối ưu hóa logic kết nối cơ sở dữ liệu để chạy mượt mà trong vòng đời serverless | 16/06/2026 | 16/06/2026 | AWS Lambda |
| 4 | - **Kiểm thử Luồng Xác thực:** <br>&emsp; + Test luồng đăng ký tài khoản dành cho student <br>&emsp; + Xác thực mã OTP gửi về email qua dịch vụ Amazon SES <br>&emsp; + Đảm bảo thông tin profile được đồng bộ chính xác vào MongoDB sau khi kích hoạt thành công | 17/06/2026 | 17/06/2026 | [Amazon Cognito](https://docs.aws.amazon.com/cognito/) |
| 5 | - **Tích hợp API Gateway:** <br>&emsp; + Cấu hình Amazon API Gateway đóng vai trò proxy điều hướng đến Lambda Backend API <br>&emsp; + Thiết lập tính năng JWT Authorizer liên kết trực tiếp với Cognito User Pool | 18/06/2026 | 18/06/2026 | Amazon API Gateway |
| 6 | - **Kiểm thử Bảo mật API Toàn diện (E2E):** <br>&emsp; + Thực hiện integration test cơ bản trên các route được bảo vệ <br>&emsp; + Kiểm tra cơ chế giải mã token, thời gian hết hạn route và xử lý lỗi cho các request không hợp lệ | 19/06/2026 | 19/06/2026 | Postman / Insomnia |

### Kết quả đạt được tuần 9:

* Thiết lập thành công luồng khép kín bao gồm đăng ký, đăng nhập và xác thực mã OTP bảo mật qua email bằng Amazon Cognito và SES.
* Tối ưu hóa chỉ mục (index) cơ sở dữ liệu thành công, đảm bảo toàn vẹn dữ liệu khi đối chiếu tài khoản qua trường định danh `cognitoSub`.
* Di chuyển thành công ứng dụng Express monolithic cũ thành một tầng API Serverless hoạt động ổn định trên AWS Lambda.
* Cấu hình thông suốt luồng phân phối traffic và kiểm tra thành công các yêu cầu (request) thông qua integration test cơ bản trên Amazon API Gateway.
* Đảm bảo cơ chế đồng bộ profile vận hành chuẩn xác, các định danh sau khi xác thực lập tức được cập nhật đầy đủ vào bộ sưu tập dữ liệu trên MongoDB.