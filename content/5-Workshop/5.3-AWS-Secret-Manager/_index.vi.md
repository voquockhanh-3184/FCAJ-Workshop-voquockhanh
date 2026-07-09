---
title : "Cấu hình AWS Secrets Manager cho Examora"
date : 2024-01-01 
weight : 3 
chapter : false
pre : " <b> 5.3. </b> "
---

Trong bước này, chúng ta sẽ cấu hình AWS Secrets Manager để lưu trữ thông tin kết nối cơ sở dữ liệu MongoDB Atlas của dự án Examora một cách an toàn.

#### 5.3.1. Mục tiêu và chuẩn bị

*   **AWS Secrets Manager** được sử dụng để lưu trữ, quản lý và truy xuất các thông tin nhạy cảm (credentials), API keys và các secret khác một cách an toàn. Dịch vụ này hỗ trợ mã hóa, quản lý quyền truy cập chi tiết, tự động xoay vòng (rotation) và kiểm tra nhật ký sử dụng (audit usage).
*   Trong phần này, chúng ta sẽ tạo một secret trong AWS Secrets Manager nhằm lưu trữ chuỗi kết nối MongoDB Atlas cho dự án Examora.
*   Secret này giúp backend Lambda có thể đọc thông tin cấu hình cơ sở dữ liệu động mà không cần phải ghi cứng (hard-code) chuỗi kết nối trong mã nguồn hoặc tệp tin môi trường `.env`.

**Yêu cầu chuẩn bị trước khi tạo secret:**
1.  Chuỗi kết nối MongoDB Atlas có dạng:
    `mongodb+srv://<username>:<password>@<cluster-url>/<DBName>?retryWrites=true&w=majority`
2.  Tên Database: **WebsiteTest2026**
3.  AWS Region: **ap-southeast-1**
4.  IAM user có quyền tạo và quản trị Secrets Manager secrets.

#### Nội dung

1. [Tạo secret trong AWS Secrets Manager](5.3.2-create-secret/)
