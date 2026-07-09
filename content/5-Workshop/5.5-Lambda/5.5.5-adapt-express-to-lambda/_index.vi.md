---
title : "Điều chỉnh backend Express để chạy trên Lambda"
date : 2024-01-01 
weight : 5
chapter : false
pre : " <b> 5.5.5. </b> "
---

Backend Express thường chạy theo mô hình server truyền thống:

Express app → server.listen(PORT)

Còn AWS Lambda không chạy ứng dụng bằng cách mở port như server mà sẽ gọi một **handler function** khi có request được gửi đến từ API Gateway. Vì vậy, backend nên được tách thành hai phần:

- Express app
  -> chứa middleware, routes, business logic

- Lambda handler
  -> nhận event từ Lambda/API Gateway và chuyển request vào Express app

**Ý tưởng xử lý:**

API Gateway event  → Lambda handler  → Express app → Middleware verify Cognito JWT
→ Connect MongoDB Atlas → Xử lý API  → Trả response

