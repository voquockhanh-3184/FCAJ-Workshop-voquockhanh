---
title: "Worklog Tuần 4"
date: 2026-05-15
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

## FCAJ WORKLOG - TUẦN 04: INFRASTRUCTURE AS CODE VỚI AWS CDK

**Thực hiện bởi:** Võ Quốc Khánh  
**Nhóm:** KQPSV Group  

---

### Mục tiêu tuần 4:

* Tìm hiểu về **Infrastructure as Code (IaC)** và cách quản lý hạ tầng AWS thông qua mã nguồn thay vì thao tác thủ công trên AWS Console.
* Chuyển đổi quy trình triển khai từ mô hình **Click-ops** sang mô hình tự động hóa bằng **AWS CDK**.
* Xây dựng và quản lý hạ tầng Serverless bằng mã nguồn, giúp:
  * Dễ dàng tái sử dụng cấu hình.
  * Đồng bộ môi trường phát triển giữa các thành viên trong nhóm.
  * Giảm thiểu sự sai lệch cấu hình trong quá trình triển khai.
* Tối ưu chi phí trong quá trình học tập và thực hành:
  * Sử dụng các tài nguyên phù hợp với AWS Free Tier.
  * Giới hạn tài nguyên Lambda như Memory và Timeout.
  * Tránh phát sinh các chi phí không cần thiết.

---

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tham khảo (Cloud Journey) |
| :--- | :--- | :--- | :--- | :--- |
| **Ngày 2** | - Tìm hiểu về Infrastructure as Code (IaC):<br>&emsp;+ Khái niệm IaC<br>&emsp;+ Lợi ích của việc quản lý hạ tầng bằng mã nguồn<br>&emsp;+ So sánh giữa Click-ops và IaC<br>&emsp;+ Tổng quan về AWS CDK | 11/05/2026 | 11/05/2026 | [Cloud Development Kit (AWS CDK) Essentials](https://000038.awsstudygroup.com) |
| **Ngày 3** | - **Thực hành: Cài đặt AWS CDK:**<br>&emsp;+ Cài đặt AWS CDK CLI thông qua npm<br>&emsp;+ Khởi tạo dự án CDK sử dụng TypeScript<br>&emsp;+ Cấu hình AWS Account và Region | 12/05/2026 | 12/05/2026 | [Cloud Development Kit (AWS CDK) Essentials](https://000038.awsstudygroup.com) |
| **Ngày 4** | - **Thực hành: Khởi tạo môi trường CDK:**<br>&emsp;+ Chạy lệnh `cdk bootstrap`<br>&emsp;+ Tạo các tài nguyên hỗ trợ cho quá trình triển khai<br>&emsp;+ Kiểm tra trạng thái môi trường CDK | 13/05/2026 | 13/05/2026 | [Infrastructure as Code Workshop Series](https://000102.awsstudygroup.com) |
| **Ngày 5** | - **Xây dựng hạ tầng Serverless bằng AWS CDK:**<br>&emsp;+ Định nghĩa DynamoDB Table bằng mã nguồn<br>&emsp;+ Cấu hình chế độ thanh toán `PAY_PER_REQUEST` cho DynamoDB<br>&emsp;+ Tạo Lambda Function<br>&emsp;+ Cấu hình Runtime, Memory, Timeout và Environment Variables | 14/05/2026 | 14/05/2026 | [AWS CDK Advanced](https://000076.awsstudygroup.com) |
| **Ngày 6** | - **Triển khai và kiểm tra hạ tầng:**<br>&emsp;+ Tạo API Gateway kết nối với Lambda<br>&emsp;+ Deploy CDK Stack lên AWS<br>&emsp;+ Kiểm tra các tài nguyên được tạo trên AWS Console | 15/05/2026 | 15/05/2026 | [AWS CDK Advanced](https://000076.awsstudygroup.com) |

---

### Kết quả đạt được tuần 4:

* Hiểu được khái niệm **Infrastructure as Code (IaC)** và vai trò của việc quản lý hạ tầng thông qua mã nguồn trong các dự án Cloud.

* Hiểu được sự khác biệt giữa:
  * Triển khai thủ công thông qua AWS Console (**Click-ops**).
  * Triển khai tự động bằng các công cụ IaC.

* Hoàn thành cài đặt và cấu hình môi trường phát triển với **AWS CDK**.

* Khởi tạo thành công dự án AWS CDK sử dụng **TypeScript** và thực hiện cấu hình môi trường bằng lệnh `cdk bootstrap`.

* Xây dựng được hạ tầng Serverless cơ bản bằng AWS CDK bao gồm:
  * Amazon DynamoDB Table.
  * AWS Lambda Function.
  * Amazon API Gateway.

* Triển khai thành công CDK Stack lên AWS và kiểm tra các tài nguyên được tạo tự động trên AWS Console.

* Hiểu được lợi ích của Infrastructure as Code trong việc:
  * Quản lý phiên bản hạ tầng.
  * Chia sẻ môi trường làm việc giữa các thành viên.
  * Tự động hóa quá trình triển khai hệ thống.