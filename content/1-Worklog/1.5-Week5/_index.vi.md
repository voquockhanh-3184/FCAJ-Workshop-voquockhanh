---
title: "Worklog Tuần 5"
date: 2026-05-22
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

## FCAJ WORKLOG - TUẦN 05: KIẾN TRÚC HƯỚNG SỰ KIỆN & ĐIỀU PHỐI QUY TRÌNH

**Thực hiện bởi:** Võ Quốc Khánh  
**Nhóm:** KQPSV Group  

---

### Mục tiêu tuần 5:

* Tìm hiểu về **Event-Driven Architecture** và cách xây dựng hệ thống xử lý bất đồng bộ trên AWS.
* Nâng cấp hệ thống từ mô hình xử lý đồng bộ sang mô hình xử lý bất đồng bộ nhằm:
  * Tăng khả năng mở rộng của hệ thống.
  * Giảm thời gian chờ của Client.
  * Xử lý các tác vụ nền (Background Tasks) hiệu quả hơn.
* Tìm hiểu cách sử dụng các dịch vụ AWS để xây dựng luồng xử lý sự kiện:
  * Amazon SNS.
  * Amazon SQS.
  * AWS Lambda.
  * AWS Step Functions.
* Xây dựng các quy trình nghiệp vụ phức tạp thông qua Workflow và State Machine.

---

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tham khảo (Cloud Journey) |
| :--- | :--- | :--- | :--- | :--- |
| **Ngày 2** | - Tìm hiểu về **Event-Driven Architecture:**<br>&emsp;+ Khái niệm Event và mô hình Event Producer/Consumer<br>&emsp;+ Mô hình xử lý bất đồng bộ (Asynchronous Processing)<br>&emsp;+ Áp dụng SNS và SQS trong hệ thống Cloud | 18/05/2026 | 18/05/2026 | [Kiến trúc hướng sự kiện (Event-Driven Architecture)](https://000054.awsstudygroup.com) |
| **Ngày 3** | - **Thực hành với Amazon SNS và SQS:**<br>&emsp;+ Tạo SNS Topic `MyTopic`<br>&emsp;+ Tạo các SQS Queue: `InventoryQueue`, `AnalyticsQueue`<br>&emsp;+ Cấu hình mô hình Fan-out Publisher/Subscriber<br>&emsp;+ Kiểm tra việc nhân bản message giữa các Queue | 19/05/2026 | 19/05/2026 | [Hệ thống Messaging với SQS và SNS](https://000077.awsstudygroup.com) |
| **Ngày 4** | - **Thực hành xử lý sự kiện với Lambda:**<br>&emsp;+ Tạo Lambda Function `ProcessOrderFunction` sử dụng Python Runtime<br>&emsp;+ Cấu hình SQS Queue làm Event Source Trigger<br>&emsp;+ Cấp quyền `AWSLambdaSQSQueueExecutionRole`<br>&emsp;+ Kiểm tra log xử lý trên CloudWatch | 20/05/2026 | 20/05/2026 | [Xử lý sự kiện với SQS và SNS](https://000083.awsstudygroup.com/) |
| **Ngày 5** | - **Tìm hiểu về AWS Step Functions:**<br>&emsp;+ Khái niệm State Machine<br>&emsp;+ Điều phối Workflow (Workflow Orchestration)<br>&emsp;+ Các trạng thái Task State, Choice State, Pass State, Fail State<br>&emsp;+ Xây dựng quy trình xử lý đơn hàng | 21/05/2026 | 21/05/2026 | [Điều phối Workflow với AWS Step Functions](https://000047.awsstudygroup.com) |
| **Ngày 6** | - **Thực hành điều phối Workflow:**<br>&emsp;+ Tạo State Machine `OrderOrchestrator`<br>&emsp;+ Kết nối Lambda `CheckStock`<br>&emsp;+ Cấu hình điều kiện rẽ nhánh bằng JSONata<br>&emsp;+ Thực thi và kiểm tra kết quả Workflow | 22/05/2026 | 22/05/2026 | [Điều phối Workflow với AWS Step Functions](https://000047.awsstudygroup.com) |

---

### Kết quả đạt được tuần 5:

* Hiểu được **Event-Driven Architecture** và cách các thành phần trong hệ thống giao tiếp với nhau thông qua Event.

* Xây dựng thành công mô hình xử lý bất đồng bộ sử dụng **Amazon SNS và Amazon SQS:**
  * Tạo SNS Topic:
    * `MyTopic`
  * Tạo các SQS Queue:
    * `InventoryQueue`
    * `AnalyticsQueue`
  * Cấu hình mô hình **Fan-out:**
    * Một message được gửi đến SNS Topic.
    * Message được nhân bản và đồng thời phân phối đến nhiều SQS Queue khác nhau.

* Xây dựng thành công hệ thống xử lý sự kiện với **AWS Lambda:**
  * Tạo Lambda Function:
    * `ProcessOrderFunction`
  * Cấu hình SQS làm **Event Source Trigger**.
  * Cấp quyền:
    * `AWSLambdaSQSQueueExecutionRole`
  * Lambda tự động nhận message từ Queue, phân tích dữ liệu JSON và thực hiện xử lý nghiệp vụ.