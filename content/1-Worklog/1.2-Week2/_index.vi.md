---
title: "Worklog Tuần 2"
date: 2026-05-01
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

## FCAJ WORKLOG - TUẦN 02: KIẾN TRÚC SERVERLESS & TÍCH HỢP HỆ THỐNG

**Thực hiện bởi:** Võ Quốc Khánh  
**Nhóm:** KQPSV Group  

---

### Mục tiêu tuần 2:

* **Hiểu về kiến trúc Serverless:** Tìm hiểu các thành phần Serverless trên AWS và cách các dịch vụ tương tác với nhau để xử lý một yêu cầu từ người dùng.
* **Nắm rõ vòng đời của một Request trong Serverless:**
  * Client gửi request đến hệ thống.
  * Amazon API Gateway tiếp nhận và định tuyến request.
  * AWS Lambda xử lý logic nghiệp vụ.
  * Amazon DynamoDB lưu trữ dữ liệu lâu dài.
* **Triển khai & Tích hợp các dịch vụ cốt lõi:**
  * HTTP API trên Amazon API Gateway.
  * AWS Lambda Function.
  * Cơ sở dữ liệu NoSQL Amazon DynamoDB.
* **Trải nghiệm phát triển:** Thực hành xây dựng ứng dụng Serverless sử dụng Node.js.

---

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tham khảo (Cloud Journey) |
| :--- | :--- | :--- | :--- | :--- |
| **Ngày 2** | - Tìm hiểu kiến trúc Serverless trên AWS.<br>- Nghiên cứu các khái niệm về Serverless Computing.<br>- Phân tích luồng hoạt động: Client → API Gateway → Lambda → DynamoDB. | 27/04/2026 | 27/04/2026 | [Serverless Backend với Lambda, S3 và DynamoDB](https://000078.awsstudygroup.com/) |
| **Ngày 3** | - Tìm hiểu kiến thức nền tảng về AWS Lambda.<br>- Nghiên cứu Lambda Function, Node.js v24 Runtime và ES Module (`.mjs`).<br>- Cấu hình Execution Role và quyền IAM Permissions. | 28/04/2026 | 28/04/2026 | [Tự động hóa Serverless với AWS Lambda](https://000022.awsstudygroup.com) |
| **Ngày 4** | - Nghiên cứu Amazon DynamoDB.<br>- Tìm hiểu cơ sở dữ liệu NoSQL, Table, Partition Key và các thao tác ghi dữ liệu. | 29/04/2026 | 29/04/2026 | [Kiến thức cơ bản về cơ sở dữ liệu NoSQL với Amazon DynamoDB](https://000060.awsstudygroup.com) |
| **Ngày 5** | - **Thực hành Lab:**<br>&emsp; + Tạo DynamoDB Table với Partition Key `userId`.<br>&emsp; + Viết Lambda Function bằng Node.js v24.<br>&emsp; + Tích hợp thư viện `@aws-sdk/client-dynamodb` để lưu trữ dữ liệu. | 30/04/2026 | 30/04/2026 | [Xây dựng CRUD Serverless với Lambda và DynamoDB](https://000133.awsstudygroup.com/) |
| **Ngày 6** | - **Thực hành Lab:**<br>&emsp; + Tạo HTTP API trên Amazon API Gateway.<br>&emsp; + Cấu hình route `POST /users` và thiết lập CORS.<br>&emsp; + Kiểm tra toàn bộ luồng tích hợp bằng công cụ `curl`. | 01/05/2026 | 01/05/2026 | [Xây dựng Serverless API](https://000066.awsstudygroup.com/) |

---

### Kết quả đạt được tuần 2:

* **Kiến thức kiến trúc:** Hiểu rõ mô hình hoạt động và các lợi ích của kiến trúc Serverless trên AWS.
* **Lưu trữ dữ liệu:** Hoàn thành việc tạo **Amazon DynamoDB** NoSQL Table sử dụng `userId` làm Partition Key.
* **Triển khai Function:** Xây dựng và triển khai thành công **AWS Lambda Function** sử dụng **Node.js v24**, áp dụng **ES Modules (`.mjs`)** và thư viện AWS SDK mới `@aws-sdk/client-dynamodb`.
* **Cấu hình API Gateway:** Triển khai thành công **API Gateway HTTP API** với route `POST /users` và kích hoạt **CORS** để cho phép các request từ bên ngoài.
* **Tích hợp End-to-End:** Kiểm tra thành công toàn bộ luồng hoạt động thông qua `curl`. Xác nhận dữ liệu từ Client được Lambda xử lý và lưu trữ thành công vào DynamoDB.