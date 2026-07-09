---
title: "Worklog Tuần 8"
date: 2026-06-12
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---


### Mục tiêu tuần 8:

* Định hướng phạm vi MVP, rà soát source code hiện tại và chốt kiến trúc AWS Serverless Hybrid cho dự án Examora.
* Xác định lộ trình triển khai chi tiết thông qua việc phân tích cấu trúc module frontend/backend.
* Chuẩn bị tài liệu kỹ thuật về mô hình hybrid và phân rã các tác vụ hạ tầng vào backlog quản lý chung.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Công cụ / Nền tảng |
| --- | --- | --- | --- | --- |
| 2 | - **Họp nhóm và Rà soát Hệ thống (Code Review):** <br>&emsp; + Đánh giá hiện trạng source code Frontend & Backend <br>&emsp; + Xác định các module có thể tái sử dụng <br>&emsp; + Phân tích giới hạn của kiến trúc cũ | 08/06/2026 | 08/06/2026 | GitHub |
| 3 | - **Tự học nhóm dịch vụ Storage:** <br>&emsp; + Tìm hiểu S3 bucket <br>&emsp; + Quản lý object key và prefix <br>&emsp; + Cấu hình CORS | 09/06/2026 | 09/06/2026 | [AWS Management Console](https://cloudjourney.awsstudygroup.com/) |
| 4 | - **Thiết kế Kiến trúc Hybrid:** <br>&emsp; + Phác thảo luồng dữ liệu giữa API Gateway, Lambda và backend cũ <br>&emsp; + Đề xuất giải pháp tích hợp cơ sở dữ liệu hiện tại lên Cloud <br>&emsp; + Xác định ranh giới (Boundaries) cho phạm vi MVP | 10/06/2026 | 10/06/2026 | Draw.io |
| 5 | - **Đọc tài liệu MongoDB Atlas Network Access:** <br>&emsp; + Nghiên cứu cách ứng dụng serverless kết nối <br>&emsp; + Triển khai kết nối qua public TLS endpoint | 11/06/2026 | 11/06/2026 | [MongoDB Atlas Dashboard](https://www.mongodb.com/docs/atlas/) |
| 6 | - **Chuẩn hóa Backlog và Thống nhất Kế hoạch:** <br>&emsp; + Phân rã sơ đồ kiến trúc thành các task hạ tầng cụ thể <br>&emsp; + Chốt danh sách các module chuyển dịch sang Serverless <br>&emsp; + Gán task triển khai cho các thành viên trong nhóm | 12/06/2026 | 12/06/2026 | Jira Software |

### Kết quả đạt được tuần 8:

* Hoàn thành định hướng phạm vi MVP cho dự án Examora một cách rõ ràng, tránh over-scoping.
* Nắm vững cấu trúc tổng thể của frontend và backend hiện tại, chỉ ra được các điểm nghẽn kỹ thuật cần tối ưu.
* Phân loại rõ ràng các module cần giữ lại và các module cần chuyển dịch sang kiến trúc AWS Serverless.
* Xây dựng, chuẩn hóa và chốt thành công backlog triển khai hạ tầng ban đầu lên công cụ quản lý tác vụ của nhóm.
* Hiểu rõ cách thức thiết lập Storage với Amazon S3 và cấu hình bảo mật network access (IP Whitelisting/TLS) kết nối đến MongoDB Atlas trong môi trường serverless.
* Hoàn thiện bản phác thảo sơ đồ kiến trúc AWS Serverless Hybrid, làm tiền đề để triển khai viết mã nguồn hạ tầng (IaC) ở tuần tiếp theo.