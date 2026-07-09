---
title : "Cấu hình JWT Authorizer và CORS cho API Gateway"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.6.3. </b> "
---

#### Mục tiêu:
*   Cấu hình **JWT Authorizer** cho API Gateway để xác thực yêu cầu API bằng token do Amazon Cognito phát hành. API Gateway sẽ kiểm tra và giải mã JWT trước khi chuyển tiếp yêu cầu vào Lambda Backend API.
*   Cấu hình **CORS** để Frontend React chạy tại môi trường local (`http://localhost:5173`) hoặc production có thể gửi yêu cầu HTTP tới API Gateway an toàn.

#### Các bước thực hiện:

1. Cấu hình JWT Authorizer:
   * Tại mục **Develop** ở menu trái -> Chọn **Authorization** -> Chọn tab **Manage authorizers** -> Nhấn **Create**.
   * Điền các thông tin cấu hình xác thực:
     * **Name**: `examora-cognito-jwt-authorizer-dev`
     * **Identity source**: `$request.header.Authorization` (API Gateway sẽ tìm JWT token tại header `Authorization`).
     * **Issuer URL**: `https://cognito-idp.ap-southeast-1.amazonaws.com/<COGNITO_USER_POOL_ID>` (Thay `<COGNITO_USER_POOL_ID>` bằng mã ID User Pool của bạn).
     * **Audience**: Nhập `<COGNITO_APP_CLIENT_ID>` (App Client ID được tạo ở phần Cognito).
   * Nhấn **Create** để khởi tạo.

   ![Tạo JWT Authorizer](/images/5-Workshop/5.6-API-Gateway/5.6.3-configure-jwt-authorizer-cors/API6.8.png)

2. Gắn Authorizer vào các route nghiệp vụ của Examora:
   * Quay lại mục **Routes** -> Nhấp chọn route `ANY /{proxy+}` (route chứa các API cần bảo mật).
   * Chọn **Attach authorization** -> Chọn đúng authorizer vừa tạo: `examora-cognito-jwt-authorizer-dev`.
   * Nhấn **Attach authorizer** -> Nhấn **Save** để lưu lại.
   * *Lưu ý*: Giữ nguyên route `GET /health` không gắn Authorizer để cho phép kiểm tra tình trạng hệ thống công khai.

   ![Gắn Authorizer cho proxy route](/images/5-Workshop/5.6-API-Gateway/5.6.3-configure-jwt-authorizer-cors/API6.9.png)

3. Cấu hình CORS:
   * Để cho phép Frontend gọi API Gateway từ một domain/port khác, chúng ta cần bật CORS.
   * Chuyển đến tab **CORS** ở menu trái -> Chọn **Configure** -> Cấu hình các thông tin (ví dụ: `Access-Control-Allow-Origin`, `Access-Control-Allow-Headers`, `Access-Control-Allow-Methods`) -> Nhấn **Save**.

   ![Cấu hình CORS](/images/5-Workshop/5.6-API-Gateway/5.6.3-configure-jwt-authorizer-cors/CORS6.1.png)

> [!NOTE]
> Hãy quay lại **Lambda Function** -> Chọn tab **Configuration** -> **Permissions** -> Cuộn xuống mục **Resource-based policy statements** để kiểm tra quyền. Đảm bảo có statement cho phép API Gateway invoke Lambda, giúp API Gateway có thể giao tiếp được với Lambda Backend API.
>
> ![Resource-based Policy](/images/5-Workshop/5.6-API-Gateway/5.6.3-configure-jwt-authorizer-cors/LambdaInvoke.png)
