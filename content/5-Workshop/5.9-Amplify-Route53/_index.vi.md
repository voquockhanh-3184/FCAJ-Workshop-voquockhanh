---
title : "AWS Amplify Hosting và Route 53"
date : 2024-01-01 
weight : 9 
chapter : false
pre : " <b> 5.9. </b> "
---

#### 5.9.1. Mục tiêu:
*   Đưa ứng dụng Frontend Examora (React/Vite) lên môi trường Internet toàn cầu bằng cách triển khai trên dịch vụ **AWS Amplify Hosting** qua phương pháp tải lên thủ công (manual deploy).
*   Cấu hình quản lý hệ thống phân giải tên miền (DNS) bằng **Amazon Route 53**.
*   Gắn tên miền tùy chỉnh (custom domain) cho ứng dụng Frontend và cấu hình bảo mật SSL/TLS.

![Sơ đồ triển khai Frontend với Amplify và Route 53](/images/5-Workshop/5.9-Amplify-Route53/5.9.1-objectives/DeployFE1.png)

#### Nội dung:
1. [Cấu hình Amazon Route 53 cho Domain](5.9.2-configure-route53/)
2. [Build và đóng gói Frontend](5.9.3-build-frontend/)
3. [Triển khai AWS Amplify Hosting](5.9.4-deploy-amplify/)
4. [Gắn Domain vào Amplify](5.9.5-configure-domain/)
