---
title : "Deploy code Backend lên Lambda"
date : 2024-01-01 
weight : 6
chapter : false
pre : " <b> 5.5.6. </b> "
---

Sau khi đã tích hợp thư viện bọc và điều chỉnh cấu trúc mã nguồn Express, chúng ta sẽ tiến hành đóng gói và triển khai ứng dụng backend lên dịch vụ AWS Lambda dưới dạng tệp tin `.zip`.

#### Các bước thực hiện:

1. Đóng gói ứng dụng (Package):
   * Trong thư mục gốc của project backend, nén toàn bộ các tệp tin và thư mục sau thành một tệp tin `.zip` (ví dụ: `backend.zip`):
     * Thư mục chứa mã nguồn: `src/` (hoặc `dist/` nếu có quá trình build/transpile).
     * Thư mục phụ thuộc: `node_modules/`.
     * Tệp cấu hình: `package.json` và `package-lock.json`.
   * *Lưu ý*: Hãy đảm bảo rằng bạn nén trực tiếp các tệp tin này chứ không phải nén thư mục cha chứa chúng, để đảm bảo cấu trúc thư mục ở mức root của file zip là chính xác.

2. Tải mã nguồn lên Lambda:
   * Truy cập trang quản lý [Functions](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/functions) của dịch vụ Lambda -> Chọn function `examora-backend-api` đã tạo -> Chọn tab **Code**.
   * Tại mục **Code source**, chọn nút **Upload from** ở góc phải -> Chọn **.zip file** -> Nhấn **Upload** và tìm đến tệp `backend.zip` vừa đóng gói -> Nhấn **Save**.

   ![Upload file .zip](/images/5-Workshop/5.5-Lambda/5.5.6-deploy-backend/LambdaNen5.1.png)

3. Cấu hình Runtime Handler:
   * Mặc định, Lambda sẽ tìm kiếm tệp `index.js` và hàm `handler` ở cấp độ gốc của thư mục. Vì mã nguồn của chúng ta nằm trong thư mục `src/` và export handler trong tệp `lambda.js` (`module.exports.handler = ...`), chúng ta cần điều chỉnh cấu hình này:
   * Cuộn xuống phần **Runtime settings** bên dưới tab Code -> Chọn **Edit**.
   * Tại ô **Handler**, chỉnh sửa giá trị thành: **`src/lambda.handler`**.
   * Bấm **Save** để lưu lại.

   ![Cấu hình Handler](/images/5-Workshop/5.5-Lambda/5.5.6-deploy-backend/LambdaNen5.2.png)
