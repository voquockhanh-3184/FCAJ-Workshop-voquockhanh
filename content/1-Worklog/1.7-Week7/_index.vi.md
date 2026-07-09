---
title: "Worklog Tuần 7"
date: 2026-06-05
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---


### Mục tiêu tuần 7:

* Thống nhất ý tưởng, chốt đề tài ứng dụng cụ thể và bắt đầu xây dựng tài liệu đề cương dự án (Proposal).
* Phác thảo thiết kế kiến trúc hệ thống tổng thể và nghiên cứu phương pháp mô hình hóa cơ sở dữ liệu NoSQL DynamoDB.
* Khởi tạo và đồng bộ môi trường làm việc chung (Kick-off) cho các thành viên trong nhóm.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Công cụ / Nền tảng |
| --- | --- | --- | --- | --- |
| 2 | - **Họp nhóm Brainstorming & Chốt đề tài:** <br>&emsp; + Thảo luận ý tưởng, đánh giá thế mạnh các thành viên để chọn đề tài thực tế <br>&emsp; + Phác thảo phạm vi dự án (Project Scope) và các tính năng cốt lõi | 01/06/2026 | 01/06/2026 | Discord |
| 3 | - **Phác thảo Kiến trúc Tổng thể:** <br>&emsp; + Thiết kế sơ đồ kiến trúc (Architecture Diagram) <br>&emsp; + Xác định luồng dữ liệu tương tác giữa Frontend (S3), API Gateway, Cognito, Lambda và DynamoDB | 02/06/2026 | 02/06/2026 | Draw.io |
| 4 | - **Khởi tạo Khung dự án (Kick-off Project):** <br>&emsp; + Tạo Repository Git chung cho nhóm <br>&emsp; + Định nghĩa bộ khung cấu trúc thư mục chuẩn bằng AWS CDK và push lên repo để cả nhóm clone về máy local | 03/06/2026 | 03/06/2026 | GitHub / AWS CDK |
| 5 | - **Xây dựng Đề cương Dự án (Proposal):** <br>&emsp; + Khởi tạo file tài liệu Proposal chi tiết <br>&emsp; + Mô tả bài toán thực tế, lập kế hoạch triển khai và phân chia công việc cụ thể cho từng thành viên | 04/06/2026 | 04/06/2026 | Google Docs |
| 6 | - **Nghiên cứu & Thiết kế DynamoDB Single-Table:** <br>&emsp; + Liệt kê các mẫu truy vấn (Access Patterns) mà Frontend yêu cầu <br>&emsp; + Áp dụng Single-Table Design, thiết kế cấu trúc khóa PK/SK với các tiền tố định danh (USER#, ORDER#) | 05/06/2026 | 05/06/2026 | NoSQL Workbench |

### Khó khăn & Cách giải quyết:

* **Vấn đề:** Các thành viên gặp khó khăn lớn khi thiết kế cơ sở dữ liệu DynamoDB do quen tư duy theo dạng bảng quan hệ (SQL), dẫn đến việc tạo quá nhiều bảng riêng lẻ gây tốn chi phí và khó tối ưu.
* **Cách giải quyết:** Nhóm tổ chức họp trực tuyến, liệt kê toàn bộ danh sách câu lệnh tìm kiếm dữ liệu mà giao diện Frontend cần. Sau đó, áp dụng kỹ thuật Single-Table Design, sử dụng tiền tố gán vào khóa PK/SK để gom toàn bộ thực thể vào chung một bảng duy nhất.

### Kết quả đạt được tuần 7:

* Thống nhất chốt đề tài và xác định rõ ràng phạm vi bài toán thực tế của dự án.
* Hoàn thành sơ đồ kiến trúc tổng thể, định hình rõ ràng luồng đi của dữ liệu xuyên suốt các dịch vụ Serverless trên AWS.
* Khởi tạo thành công tài liệu đề cương dự án (Proposal) bao gồm đầy đủ kế hoạch triển khai và bảng phân vai nhiệm vụ chi tiết.
* Xây dựng xong bản phác thảo cấu trúc bảng DynamoDB theo phương pháp Single-Table Design, giải quyết triệt để bài toán tối ưu chi phí và truy vấn dữ liệu phức tạp.
* Thiết lập cấu trúc thư mục dự án đồng bộ thông qua AWS CDK và phân phối thành công mã nguồn khung đến máy local của toàn bộ thành viên.