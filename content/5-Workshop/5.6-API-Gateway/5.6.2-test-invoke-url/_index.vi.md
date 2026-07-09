---
title : "Test các Invoke URL của API Gateway đã tạo"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.6.2. </b> "
---

Sau khi tạo xong API Gateway, chúng ta tiến hành kiểm tra URL invoke công khai để đảm bảo API Gateway kết nối thành công tới Lambda và trả về kết quả chính xác từ Express application.

#### Các bước thực hiện:

1. Lấy URL Invoke:
   * Tại menu quản lý API Gateway bên trái -> Chọn mục **Deploy** -> Chọn **Stages**.
   * Chọn stage **`$default`** trong danh sách -> Sao chép giá trị tại trường **Invoke URL**.

   ![Lấy Invoke URL](/images/5-Workshop/5.6-API-Gateway/5.6.2-test-invoke-url/API6.6.png)

2. Kiểm tra Route `/health`:
   * Sử dụng trình duyệt web, Postman hoặc cURL, dán URL vừa copy vào và thêm hậu tố `/health` (ví dụ: `https://<api-id>.execute-api.ap-southeast-1.amazonaws.com/health`).
   * **Kết quả mong đợi**: Trả về dữ liệu JSON dạng `{"status":"OK"}` hoặc tương tự như cấu hình trong Express app backend. Điều này chứng minh luồng đi từ API Gateway tới Lambda hoạt động thông suốt.

   ![Kết quả Test Invoke URL thành công](/images/5-Workshop/5.6-API-Gateway/5.6.2-test-invoke-url/API6.7.png)
