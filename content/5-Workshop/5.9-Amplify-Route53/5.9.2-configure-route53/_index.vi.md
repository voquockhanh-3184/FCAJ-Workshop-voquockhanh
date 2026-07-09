---
title : "Cấu hình Amazon Route 53 cho Domain"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.9.2. </b> "
---

#### Các bước thực hiện:

1. Khởi tạo Hosted Zone trên Amazon Route 53:
   * Truy cập dịch vụ **Amazon Route 53** -> Chọn **Hosted zones** ở menu bên trái -> Nhấn **Create hosted zone**.
   * Nếu chưa có domain, chọn *Register a domain* để mua tên miền trực tiếp trên AWS.
   * Nếu đã sở hữu domain mua từ nhà cung cấp khác (ví dụ: Namecheap, Mắt Bão, GoDaddy,...):
     * **Domain name**: Nhập tên domain của bạn (ví dụ: `examora.click`).
     * **Type**: Chọn `Public hosted zone`.
     * Chọn **Create hosted zone** để khởi tạo vùng cấu hình DNS.

   ![Truy cập Route 53 Hosted Zone](/images/5-Workshop/5.9-Amplify-Route53/5.9.2-configure-route53/Route1.png)

   ![Khởi tạo Hosted Zone thành công](/images/5-Workshop/5.9-Amplify-Route53/5.9.2-configure-route53/Route2.png)

2. Lấy danh sách AWS Name Servers:
   * Bấm vào tên miền vừa cấu hình trong bảng danh sách Hosted zones.
   * Tại tab **Records**, tìm bản ghi loại `NS` (Name Server) -> Ghi lại danh sách **4 giá trị Name Servers** của AWS được hiển thị.

   ![Lấy danh sách Name Servers AWS](/images/5-Workshop/5.9-Amplify-Route53/5.9.2-configure-route53/Route3.png)

3. Cấu hình Name Servers tại nhà cung cấp tên miền:
   * Đăng nhập vào trang quản trị tên miền nơi bạn mua domain.
   * Tìm mục cài đặt **Custom DNS** hoặc **Custom Name Servers**.
   * Thay thế các địa chỉ Name Servers cũ của nhà cung cấp bằng **4 giá trị AWS Name Servers** vừa copy ở bước trên -> Lưu lại.

4. Kiểm tra cập nhật DNS Name Servers:
   * Mở Terminal (Command Prompt) trên máy tính cá nhân và chạy lệnh kiểm tra:
     ```bash
     nslookup -type=NS <tên_domain>
     ```
     *(Ví dụ: `nslookup -type=NS examora.click`)*.
   * Nếu kết quả trả về đúng danh sách nameserver chứa `awsdns`, tên miền của bạn đã được Route 53 quản lý DNS thành công.

   ![Kiểm tra DNS với lệnh nslookup](/images/5-Workshop/5.9-Amplify-Route53/5.9.2-configure-route53/Route4.png)
