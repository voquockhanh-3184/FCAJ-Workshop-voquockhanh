---
title: "Worklog Tuần 3"
date: 2026-05-08
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

## FCAJ WORKLOG - TUẦN 03: XÁC THỰC NGƯỜI DÙNG & QUẢN LÝ DANH TÍNH

**Thực hiện bởi:** Võ Quốc Khánh  
**Nhóm:** KQPSV Group  

---

### Mục tiêu tuần 3:

* Nghiên cứu và triển khai hệ thống quản lý danh tính người dùng (Authentication) trên AWS.
* Tích hợp Amazon Cognito để cung cấp các chức năng:
  * Đăng ký tài khoản người dùng.
  * Đăng nhập người dùng.
  * Quản lý danh tính người dùng.
  * Cấp phát JWT Authentication Token.
* Thiết lập bảo mật cho Serverless API bằng cách kết nối Amazon Cognito với Amazon API Gateway.
* Hoàn thiện kết nối giữa Frontend và Backend thông qua cơ chế xác thực người dùng.

---

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tham khảo (Cloud Journey) |
| :--- | :--- | :--- | :--- | :--- |
| **Ngày 2** | - Tìm hiểu về Amazon Cognito:<br>&emsp;+ User Pool<br>&emsp;+ Identity Pool<br>&emsp;+ Authentication Flow<br>&emsp;+ JWT Token | 04/05/2026 | 04/05/2026 | [Xác thực người dùng với Amazon Cognito](https://000081.awsstudygroup.com/) |
| **Ngày 3** | - **Thực hành:**<br>&emsp;+ Tạo Cognito User Pool<br>&emsp;+ Cấu hình đăng nhập bằng Email<br>&emsp;+ Tạo App Client cho ứng dụng Single-page Application (SPA)<br>&emsp;+ Cấu hình Cognito Hosted UI | 05/05/2026 | 05/05/2026 | [Xác thực cho ứng dụng Single Page Application](https://000055.awsstudygroup.com) |
| **Ngày 4** | - **Thực hành:**<br>&emsp;+ Tạo Identity Pool<br>&emsp;+ Cấu hình IAM Role cho người dùng đã xác thực<br>&emsp;+ Thiết lập Authenticated Role để chuẩn bị cơ chế phân quyền truy cập tài nguyên AWS | 06/05/2026 | 06/05/2026 | [Xác thực đa miền với Amazon Cognito](https://000141.awsstudygroup.com) |
| **Ngày 5** | - Bảo mật API Gateway bằng Cognito Authorizer:<br>&emsp;+ Tạo JWT Authorizer<br>&emsp;+ Cấu hình Issuer URL từ Cognito User Pool<br>&emsp;+ Kiểm tra Audience thông qua App Client ID<br>&emsp;+ Áp dụng Authorizer cho API Route | 07/05/2026 | 07/05/2026 | [Tích hợp Frontend với API Gateway](https://000135.awsstudygroup.com/) |
| **Ngày 6** | - **Thực hành tích hợp Frontend:**<br>&emsp;+ Cấu hình OAuth 2.0 Flow<br>&emsp;+ Kiểm tra chức năng đăng ký/đăng nhập thông qua Hosted UI<br>&emsp;+ Lấy JWT ID Token<br>&emsp;+ Chuẩn bị gửi Token thông qua Header Authorization khi gọi API | 08/05/2026 | 08/05/2026 | [Lưu trữ Serverless và Authentication với AWS Amplify](https://000134.awsstudygroup.com/) |

---

### Kết quả đạt được tuần 3:

* Hiểu được cơ chế **Authentication và Authorization** trong hệ thống Serverless sử dụng Amazon Cognito.

* Hoàn thành cấu hình Amazon Cognito:
  * Tạo User Pool để quản lý tài khoản người dùng.
  * Cấu hình xác thực thông qua Email.
  * Tạo App Client dành cho ứng dụng Single-page Application (SPA).
  * Thiết lập Cognito Hosted UI để hỗ trợ đăng ký và đăng nhập.

* Hoàn thành việc tạo Identity Pool:
  * Kết nối Identity Pool với User Pool.
  * Cấu hình IAM Role cho người dùng đã xác thực.
  * Chuẩn bị cơ chế cấp quyền truy cập tài nguyên AWS.

* Bảo mật thành công API Gateway bằng Cognito JWT Authorizer:
  * Tạo Authorizer trên HTTP API Gateway.
  * Cấu hình Issuer URL liên kết với Cognito User Pool.
  * Kiểm tra Audience thông qua App Client ID.
  * Áp dụng xác thực cho các API Route như `POST /users`.

* Hoàn thiện tích hợp luồng xác thực giữa Frontend và Backend:
  * Đăng ký và đăng nhập thành công thông qua Cognito Hosted UI.
  * Lấy được JWT ID Token sau khi xác thực.
  * Chuẩn bị Token để gửi trong Header `Authorization` khi thực hiện gọi API.

---

### Vấn đề gặp phải & Cách giải quyết:

* **Vấn đề:** Không thể lấy trực tiếp JWT ID Token sau khi đăng nhập thông qua Cognito Hosted UI.

* **Nguyên nhân:**
  * Cognito App Client mặc định sử dụng OAuth 2.0 Authorization Code Grant.
  * Sau khi đăng nhập thành công, trình duyệt chỉ trả về Authorization Code dưới dạng: