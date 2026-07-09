---
title : "Giới thiệu"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

### Chuẩn bị tài nguyên

#### 1. Phạm vi tài nguyên sử dụng

**Examora - Online Exam Platform** được triển khai theo hướng **Console-first, SAM-lite optional**. Nhóm sẽ cấu hình tài nguyên chính trên **AWS Management Console** trước để chụp ảnh step by step cho workshop giúp mọi người có thể hiểu rõ từng bước cài đặt, cấu hình dịch vụ. Sau đó, nhóm sẽ sử dụng **AWS SAM-lite** để mô tả lại một phần tài nguyên serverless bằng Infrastructure as Code.

**Examora** sử dụng các dịch vụ sau:

| Nhóm | Dịch vụ |
|---|---|
| Authentication | Amazon Cognito, Amazon SES |
| Backend API | AWS Lambda, Amazon API Gateway |
| Database external | MongoDB Atlas |
| Secret/config | AWS Secrets Manager |
| Async grading | Amazon SQS, AWS Lambda |
| File upload/import | Amazon S3, AWS Lambda |
| Frontend hosting | AWS Amplify Hosting |
| DNS / Custom domain | Amazon Route 53 |
| Monitoring | Amazon CloudWatch Logs, AWS X-Ray |
| Permission | AWS IAM |


