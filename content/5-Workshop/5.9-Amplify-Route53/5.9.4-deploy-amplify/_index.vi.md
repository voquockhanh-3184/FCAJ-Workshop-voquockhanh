---
title : "Triển khai AWS Amplify Hosting"
date : 2024-01-01 
weight : 4
chapter : false
pre : " <b> 5.9.4. </b> "
---

#### Các bước thực hiện:

1. Triển khai gói Frontend lên Amplify:
   * Trên thanh tìm kiếm AWS Console -> Tìm dịch vụ **AWS Amplify**.
   * Nhấn **Create new app**.
   * Tại mục *Start building with Amplify* -> Chọn **Deploy without Git** -> Nhấn **Next**.

   ![Chọn Deploy without Git](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/Amplify1.png)

   * Nhập thông tin app:
     * **App name**: Đặt tên ứng dụng (ví dụ: `examora-frontend`).
     * **Branch name**: Nhập tên nhánh (ví dụ: `main`).
     * **Method**: Kéo thả tệp tin nén `.zip` của frontend vừa đóng gói ở bước 5.9.3 vào khung tải lên.
   * Nhấn **Save and deploy** để bắt đầu quá trình triển khai thủ công.

   ![Tải lên file zip và Deploy](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/Amplify2.png)

   * Sau khi quá trình Deploy hoàn tất thành công, bạn sẽ nhận được thông báo trạng thái Deploy thành công kèm một đường dẫn domain mặc định của AWS Amplify có cấu trúc dạng: `https://main.xxxxxx.amplifyapp.com`.

   ![Deploy hoàn tất thành công](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/Amplify3.png)

   * Bấm vào đường dẫn mặc định này. Nếu trang đăng nhập của Examora hiển thị và hoạt động thì ứng dụng Frontend đã được deploy chính xác trên AWS.

   ![Truy cập trang đăng nhập qua domain Amplify](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/Amplify4.png)

2. Cấu hình Rewrites and Redirects cho Single Page Application (SPA):
   * Do ứng dụng React sử dụng thư viện **React Router** để định tuyến (Client-side routing), chúng ta cần cấu hình để mọi request URL lạ đều được chuyển về `index.html` xử lý.
   * Tại menu bên trái của ứng dụng Amplify -> Chọn mục **Hosting** -> Chọn **Rewrites and redirects** -> Nhấp vào **Manage redirects**.

   ![Vào cài đặt Rewrites and redirects](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/Amplify5.png)

   * Nhấn **Add rule** hoặc sửa lại rule mặc định của SPA thành cấu trúc:
   * Nhấn **Save** để lưu lại quy tắc cấu hình. Điều này giúp các route con (ví dụ: `/dang-nhap`, `/lich-su-thi`) không bị báo lỗi 404 khi tải lại trang.

   ![Cấu hình các rules redirect](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/Amplify6.png)

   ![Lưu thành công các rules](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/Amplify7.png)

3. Cấu hình lại CORS trong API Gateway:
   * Do Frontend đã được chuyển lên domain mới của AWS Amplify, chúng ta cần bổ sung domain này vào danh sách được phép gọi API (CORS) của API Gateway để không bị lỗi bảo mật CORS.
   * Truy cập **API Gateway** -> Chọn API `examora-api` -> Chọn mục **CORS** -> Nhấn **Configure**.
   * Tại mục **Access-Control-Allow-Origin** -> Nhập thêm domain mặc định của Amplify vừa sinh ra ở bước 1 -> Nhấn **Save**.

   ![Cấu hình CORS API Gateway](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/CORS5.9.png)

4. Cập nhật biến môi trường cho Lambda Backend API:
   * Truy cập **Lambda** -> Chọn hàm `examora-backend-api` -> Chọn tab **Configuration** -> **Environment variables** -> Bấm **Edit**.
   * Cập nhật biến `FRONTEND_ORIGIN` bằng giá trị URL của Amplify app.
   * Bấm **Save**.

   ![Cập nhật biến môi trường Lambda](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/LambdaBE5.9.png)

5. Triển khai lại và kiểm tra toàn diện:
   * Tiến hành nén file `.zip` của Frontend chứa các cấu hình kết nối API Gateway mới và tải lên (Upload) lại lên Amplify.
   * Truy cập website qua domain mặc định của Amplify, tiến hành đăng nhập và thực hiện làm bài thi thử để kiểm tra các luồng API kết nối bình thường.

   ![Kiểm tra hoạt động toàn diện website](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/TestAmplify1.png)
