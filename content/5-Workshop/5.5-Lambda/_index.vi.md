---
title : "Tạo Lambda Backend API cho Examora"
date : 2024-01-01 
weight : 5 
chapter : false
pre : " <b> 5.5. </b> "
---

Trong bước này, chúng ta sẽ cấu hình **AWS Lambda** để triển khai backend Express của **Examora**, thay thế cho mô hình máy chủ truyền thống nhằm tối ưu chi phí và tăng khả năng mở rộng.

#### 5.5.1. Mục tiêu

Sử dụng dịch vụ **AWS Lambda** làm Backend API để xử lý các nghiệp vụ chính của hệ thống bao gồm: quản lý thông tin người dùng, lớp học, đề thi, câu hỏi, bài làm, kết quả, cũng như hỗ trợ các API upload/import dữ liệu.

Lambda Backend API sẽ thực hiện:
*   Nhận yêu cầu (request) từ API Gateway.
*   Xử lý logic nghiệp vụ của hệ thống Examora.
*   Đọc MongoDB Connection URI từ AWS Secrets Manager.
*   Kết nối và truy vấn cơ sở dữ liệu MongoDB Atlas.
*   Ghi nhật ký hoạt động (logs) vào CloudWatch.
*   Hỗ trợ theo dõi đường đi của request (tracing) bằng AWS X-Ray.

![Kiến trúc hoạt động của Lambda Backend](/images/5-Workshop/5.5-Lambda/5.5.2-create-iam-role/LambdaBE5.1.png)

#### Nội dung

1. [Tạo IAM Role cho Lambda Backend API](5.5.2-create-iam-role/)
2. [Tạo Lambda Function](5.5.3-create-lambda-function/)
3. [Cấu hình Environment Variables cho Lambda Function](5.5.4-configure-environment-variables/)
4. [Điều chỉnh backend Express để chạy trên Lambda](5.5.5-adapt-express-to-lambda/)
5. [Deploy code Backend lên Lambda](5.5.6-deploy-backend/)
6. [Test Lambda trực tiếp trước khi gắn API Gateway](5.5.7-test-lambda/)
