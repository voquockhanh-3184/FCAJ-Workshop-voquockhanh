---
title: "Worklog Tuần 6"
date: 2026-05-29
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

---

### Mục tiêu tuần 6:

* Nghiên cứu và triển khai hệ thống giám sát tập trung trên AWS nhằm theo dõi trạng thái hoạt động của ứng dụng, thu thập log và hỗ trợ quá trình phân tích lỗi.

* Làm quen với các công cụ giám sát và phân tích lỗi:

  * Amazon CloudWatch.
  * AWS X-Ray.

* Xây dựng quy trình **Continuous Integration và Continuous Deployment (CI/CD)** nhằm:

  * Tự động kiểm tra mã nguồn.
  * Tự động build ứng dụng.
  * Tự động triển khai hạ tầng lên AWS.

* Chuẩn hóa quy trình làm việc nhóm bằng cách tích hợp CI/CD với hệ thống quản lý mã nguồn.

---

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| Thứ 2 | - Nghiên cứu hệ thống Monitoring trên AWS:<br>&emsp; + Amazon CloudWatch Logs<br>&emsp; + Log Groups và Log Streams<br>&emsp; + Giám sát trạng thái hoạt động của Lambda và API Gateway<br>&emsp; + Phân tích lỗi thông qua Logs | 25/05/2026 | 25/05/2026 | [Tài liệu AWS CloudWatch](https://000008.awsstudygroup.com/) |
| Thứ 3 | - **Thực hành AWS X-Ray:**<br>&emsp; + Kích hoạt Distributed Tracing<br>&emsp; + Theo dõi luồng xử lý request giữa các dịch vụ<br>&emsp; + Phân tích độ trễ (Latency)<br>&emsp; + Xác định các điểm nghẽn trong hệ thống | 26/05/2026 | 26/05/2026 | [Tài liệu AWS X-Ray](https://000140.awsstudygroup.com/3-build-frontend-pipeline/) |
| Thứ 4 | - Nghiên cứu CI/CD Pipeline:<br>&emsp; + Khái niệm Continuous Integration và Continuous Deployment<br>&emsp; + Quy trình tự động build, test và deploy<br>&emsp; + Tổng quan về GitHub Actions / AWS CodePipeline | 27/05/2026 | 27/05/2026 | [Tài liệu AWS CI/CD](https://000017.awsstudygroup.com/) |
| Thứ 5 | - **Thực hành xây dựng Pipeline:**<br>&emsp; + Tạo file cấu hình CI/CD Workflow<br>&emsp; + Cấu hình trigger khi merge code vào nhánh `main`<br>&emsp; + Kiểm tra mã nguồn (Linting)<br>&emsp; + Thực hiện build và kiểm thử tự động | 28/05/2026 | 28/05/2026 | [Tài liệu GitHub Actions](https://000017.awsstudygroup.com/) |
| Thứ 6 | - **Triển khai tự động lên AWS:**<br>&emsp; + Cấu hình AWS Credentials cho Pipeline<br>&emsp; + Kết nối CI/CD với AWS CDK<br>&emsp; + Tự động triển khai Infrastructure lên AWS<br>&emsp; + Kiểm tra kết quả triển khai | 29/05/2026 | 29/05/2026 | [Tài liệu AWS CDK](https://000017.awsstudygroup.com/) |

---

### Kết quả đạt được tuần 6:

* Hiểu được vai trò của hệ thống **Monitoring** trong quá trình vận hành ứng dụng Cloud.

* Hoàn thành cấu hình **Amazon CloudWatch:**

  * Thu thập log tập trung cho AWS Lambda.
  * Theo dõi log thực thi của API Gateway.
  * Phân tích lỗi thông qua CloudWatch Logs.

* Hoàn thành kích hoạt và sử dụng **AWS X-Ray:**

  * Theo dõi luồng xử lý request giữa các dịch vụ.
  * Quan sát Service Map của Distributed Tracing.
  * Phân tích độ trễ của từng thành phần trong hệ thống.
  * Hỗ trợ xác định các điểm nghẽn trong quá trình xử lý.

* Xây dựng thành công quy trình **CI/CD Pipeline:**

  * Tạo file cấu hình Pipeline.
  * Thiết lập trigger tự động khi có thay đổi trên nhánh `main`.
  * Tự động thực hiện các bước:
    * Kiểm tra chất lượng mã nguồn (Linting).
    * Chạy kiểm thử (Testing).
    * Build ứng dụng.
    * Triển khai Infrastructure bằng AWS CDK.

* Hoàn thiện quy trình triển khai tự động, giảm thiểu thao tác thủ công và đảm bảo môi trường triển khai nhất quán giữa các thành viên trong nhóm.