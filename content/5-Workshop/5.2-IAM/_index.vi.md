---
title : "Thiết lập IAM cho Examora"
date : 2024-01-01 
weight : 2 
chapter : false
pre : " <b> 5.2. </b> "
---

Trong bước này, chúng ta sẽ cấu hình IAM để chuẩn bị tài khoản AWS cho dự án **Examora - Online Exam Platform.**

#### 5.2.1. Mục tiêu

**IAM** trong Examora đóng 2 vai trò chính:

> **a. Quyền truy cập cho con người (Human access)**
> Người phát triển đăng nhập AWS Console để khởi tạo, quản lý và kiểm tra các tài nguyên.
>
> **b. Quyền truy cập cho ứng dụng/hệ thống (Workload access)**
> Các dịch vụ AWS Lambda, API Gateway và các dịch vụ khác sử dụng IAM Role để giao tiếp và truy cập an toàn tới AWS Secrets Manager, Amazon S3, Amazon SQS, Amazon CloudWatch.

#### Nội dung

1. [Tạo Account Alias AWS](5.2.2-create-account-alias/)
2. [Tạo nhóm quản trị IAM](5.2.3-create-admin-group/)
3. [Tạo IAM User và bật MFA để thao tác trên AWS Console](5.2.4-create-iam-user/)
4. [Gắn IAM permission policy](5.2.5-attach-policy/)
