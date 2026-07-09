---
title : "Kiểm tra API Gateway"
date : 2024-01-01 
weight : 4
chapter : false
pre : " <b> 5.6.4. </b> "
---

#### Testcase 1: Gọi `/api/auth/me` không có token
*   **Kết quả mong đợi**: Trả về mã lỗi `401 Unauthorized` từ API Gateway.
*   **Kết quả thực tế**:

   ![Testcase 1](/images/5-Workshop/5.6-API-Gateway/5.6.4-test-api-gateway/TestAPI1.png)

*   *Đánh giá*: Cognito JWT Authorizer đang hoạt động và chặn các yêu cầu không đính kèm token hợp lệ một cách chính xác.

---

#### Testcase 2: Gọi `/api/auth/me` có Cognito JWT
*   Truy cập Frontend ở local, đăng nhập tài khoản Cognito thành công.
*   Mở trình duyệt DevTools (F12) -> Chọn tab **Console** và thực thi đoạn mã test sau:

```javascript
fetch("https://4js2c8rp18.execute-api.ap-southeast-1.amazonaws.com/api/auth/me", {
  headers: {
    Authorization: `Bearer ${localStorage.getItem("token")}`
  }
})
  .then(async res => {
    console.log("status", res.status);
    console.log(await res.text());
  })
  .catch(console.error);
```

*   **Kết quả mong đợi**: Trả về dữ liệu profile người dùng dạng JSON từ MongoDB.
*   **Kết quả thực tế**:

   ![Testcase 2](/images/5-Workshop/5.6-API-Gateway/5.6.4-test-api-gateway/TestAPI2.png)

*   *Đánh giá*: Kết quả cho thấy API Gateway đã gọi thành công Lambda Backend API với JWT Cognito hợp lệ. Route `/api/auth/me` trả về đúng profile người dùng từ cơ sở dữ liệu MongoDB Atlas.
*   *Kết luận*: Luồng xác thực: **Cognito -> API Gateway JWT Authorizer -> Lambda -> MongoDB** đã hoạt động hoàn toàn chính xác.

Sau đó, chúng ta chỉ cần cập nhật lại biến môi trường endpoint API Gateway cho Frontend.
