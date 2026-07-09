---
title : "Gắn Domain vào Amplify"
date : 2024-01-01 
weight : 5
chapter : false
pre : " <b> 5.9.5. </b> "
---

#### Các bước thực hiện:

1. Thiết lập Custom Domain trên Amplify app:
   * Mở giao diện quản trị ứng dụng của bạn trên **AWS Amplify**.
   * Tại thanh menu bên trái, phần **Hosting** -> Chọn mục **Custom domains** -> Chọn **Add domain**.

   ![Chọn Custom domains](/images/5-Workshop/5.9-Amplify-Route53/5.9.5-configure-domain/GanDomain1.png)

2. Chọn Domain và Cấu hình:
   * Chọn đúng domain đã cấu hình trong Route 53 từ trước (ví dụ: `examora.click`).
   * Bấm **Configure domain**.

   ![Chọn domain đã quản lý bởi Route 53](/images/5-Workshop/5.9-Amplify-Route53/5.9.5-configure-domain/GanDomain2.png)

   * Cấu hình ánh xạ subdomain (Subdomain mapping):
     * Cấu hình chuyển hướng domain gốc (ví dụ: `examora.click` trỏ về nhánh `main`).
     * Thiết lập subdomain `www` (ví dụ: `www.examora.click` trỏ về nhánh `main`).
   * Chọn **Save** (hoặc **Add domain**) và chờ đợi hệ thống thiết lập. Hệ thống sẽ tự động tạo chứng chỉ SSL/TLS miễn phí qua AWS Certificate Manager (ACM) và trỏ các bản ghi DNS cần thiết trong Route 53 cho bạn.

   ![Cấu hình Subdomain mapping](/images/5-Workshop/5.9-Amplify-Route53/5.9.5-configure-domain/GanDomain3.png)

   * Đợi quá trình xác thực SSL và cấu hình DNS hoàn tất. Khi thấy cột **Status** chuyển sang trạng thái màu xanh **Available**, tên miền tùy chỉnh đã được kích hoạt thành công.

   ![Tên miền tùy chỉnh sẵn sàng hoạt động](/images/5-Workshop/5.9-Amplify-Route53/5.9.5-configure-domain/GanDomain4.png)

3. Cập nhật CORS trong API Gateway cho Custom Domain:
   * Khi sử dụng tên miền tùy chỉnh, chúng ta cần cấp quyền truy cập API cho các địa chỉ domain mới.
   * Truy cập **API Gateway** -> Chọn API `examora-api` -> Chọn mục **CORS** -> Chọn **Configure**.
   * Thêm hai địa chỉ domain tùy chỉnh mới vào danh sách **Access-Control-Allow-Origin**:
     * `https://examora.click`
     * `https://www.examora.click`
   * Bấm **Save** để lưu lại.

   ![Bổ sung domain tùy chỉnh vào CORS](/images/5-Workshop/5.9-Amplify-Route53/5.9.5-configure-domain/GanDomain5.png)

4. Cập nhật biến môi trường cho Lambda Backend API:
   * Truy cập dịch vụ **Lambda** -> Chọn hàm `examora-backend-api` -> Chuyển qua tab **Configuration** -> **Environment variables** -> Bấm **Edit**.
   * Cập nhật lại giá trị biến `FRONTEND_ORIGIN` thành tên miền tùy chỉnh chính thức của bạn (ví dụ: `https://www.examora.click` hoặc `https://examora.click`).
   * Nhấn **Save** để lưu cấu hình.

   ![Cập nhật biến môi trường Lambda](/images/5-Workshop/5.9-Amplify-Route53/5.9.5-configure-domain/GanDomain6.png)

5. Truy cập kiểm tra thực tế:
   * Mở trình duyệt và truy cập các địa chỉ: `https://www.examora.click` hoặc `https://examora.click`.
   
   ![Truy cập website qua Custom Domain thành công](/images/5-Workshop/5.9-Amplify-Route53/5.9.5-configure-domain/GanDomain7.png)

Như vậy, nhóm đã kết hợp sử dụng thành công các dịch vụ hạ tầng đám mây AWS để xây dựng, vận hành và triển khai ứng dụng thi trắc nghiệm trực tuyến **Examora** một cách ổn định, bảo mật và tối ưu hóa chi phí serverless.
