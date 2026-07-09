---
title : "Tạo API Gateway cho Lambda Backend API"
date : 2024-01-01 
weight : 6 
chapter : false
pre : " <b> 5.6. </b> "
---

#### Mục tiêu:

Ta sẽ tạo public API endpoint để frontend gọi backend. API Gateway sẽ validate JWT từ Cognito bằng JWT Authorizer, sau đó route request hợp lệ đến Lambda (Backend API).

API Gateway đóng vai trò:
*   Nhận request HTTP từ frontend.
*   Kiểm tra JWT do Cognito phát hành.
*   Chặn request không hợp lệ trước khi vào Lambda.
*   Route request hợp lệ đến Lambda Backend API.
*   Cấu hình CORS để frontend local/prod gọi API được.

Sau bước này, frontend có thể gọi backend qua URL dạng:
`https://<api-id>.execute-api.ap-southeast-1.amazonaws.com`

#### Nội dung:
1. [Tạo HTTP API và gắn Lambda Backend](5.6.1-create-http-api/)
2. [Test các Invoke URL của API Gateway đã tạo](5.6.2-test-invoke-url/)
3. [Cấu hình JWT Authorizer và CORS cho API Gateway](5.6.3-configure-jwt-authorizer-cors/)
4. [Kiểm tra API Gateway](5.6.4-test-api-gateway/)
