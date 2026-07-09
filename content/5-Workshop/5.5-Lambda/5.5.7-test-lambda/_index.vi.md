---
title : "Test Lambda trực tiếp trước khi gắn API Gateway"
date : 2024-01-01 
weight : 7
chapter : false
pre : " <b> 5.5.7. </b> "
---

Trước khi cấu hình API Gateway để phân phối request từ ngoài Internet, chúng ta có thể thực hiện kiểm thử (test) trực tiếp trên AWS Lambda Console bằng cách giả lập một API Gateway event.

#### Các bước thực hiện:

1. Tạo Event Test giả lập:
   * Trên trang chi tiết Lambda Function `examora-backend-api` -> Chọn tab **Test**.
   * Cấu hình sự kiện kiểm thử mới:
     * **Test event action**: Chọn **Create new event**.
     * **Event name**: Nhập tên sự kiện (ví dụ: `TestHealthGet`).
     * **Template**: Giữ nguyên `hello-world` hoặc chọn `apigateway-aws-proxy`.
     * **Event JSON**: Sao chép và paste đoạn JSON giả lập API Gateway HTTP API payload v2 dưới đây:

   ```json
   {
     "version": "2.0",
     "routeKey": "GET /health",
     "rawPath": "/health",
     "rawQueryString": "",
     "headers": {
       "host": "example.com",
       "user-agent": "lambda-test"
     },
     "requestContext": {
       "http": {
         "method": "GET",
         "path": "/health"
       }
     },
     "isBase64Encoded": false
   }
   ```

   ![Tạo Event Test](/images/5-Workshop/5.5-Lambda/5.5.6-deploy-backend/LambdaNen5.3.png)

2. Thực thi kiểm thử (Test Execution):
   * Nhấn nút **Test** ở góc phải trên.
   * Kiểm tra kết quả trả về trong phần **Execution result**:
     * Nếu **statusCode** trả về là **`200`** và body chứa chuỗi JSON mong muốn (ví dụ: `{"status":"OK"}`), tức là Express app đã khởi động và hoạt động bình thường trên AWS Lambda.

   ![Kết quả kiểm thử thành công](/images/5-Workshop/5.5-Lambda/5.5.6-deploy-backend/LambdaNen5.4.png)

3. Kiểm tra Logs thực thi trong Amazon CloudWatch:
   * AWS Lambda tự động tích hợp với CloudWatch để ghi nhật ký hoạt động.
   * Chọn tab **Monitor** trên trang chi tiết Lambda -> Chọn **View CloudWatch logs**.
   * Tại trang CloudWatch Logs, mở **Log Stream** mới nhất để xem chi tiết thông tin log kết nối MongoDB, thời gian khởi động, dung lượng bộ nhớ sử dụng thực tế và mã định danh của request (Request ID).

   ![Kiểm tra CloudWatch Logs](/images/5-Workshop/5.5-Lambda/5.5.6-deploy-backend/CloudWatchLog.png)

   * **CloudWatch Logs** đóng vai trò cực kỳ quan trọng trong môi trường serverless để phục vụ cho việc debug, tối ưu chi phí (theo dõi thời gian thực thi / Memory tối đa sử dụng) và giám sát hệ thống.

#### Tóm tắt:
Chúng ta đã triển khai thành công dịch vụ **AWS Lambda** (Backend API), đóng gói ứng dụng Express chạy ổn định trên môi trường FaaS (Function-as-a-Service) và kết nối an toàn tới MongoDB Atlas thông qua Secrets Manager.
