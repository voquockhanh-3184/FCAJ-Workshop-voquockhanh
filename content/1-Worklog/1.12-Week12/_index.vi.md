---
title: "Worklog Tuần 12"
date: 2026-07-06
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---


### Mục tiêu tuần 12:

* Triển khai mã nguồn frontend lên AWS Amplify Hosting và chuẩn bị cấu hình domain/hệ thống phân giải AWS Route 53.
* Hoàn thiện quy trình kiểm thử toàn diện, đóng gói tài liệu dự án (proposal) và viết báo cáo workshop theo kiến trúc serverless mới.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Công cụ / Nền tảng |
| --- | --- | --- | --- | --- |
| 2 | - **Xác thực Đóng gói Frontend:** <br>&emsp; + Kiểm tra quá trình đóng gói ứng dụng frontend ở môi trường production bằng lệnh `npm run build` <br>&emsp; + Xác nhận thư mục kết xuất `dist/` có chứa file `index.html` và đầy đủ các thư mục assets cần thiết | 06/07/2026 | 06/07/2026 | Vite Documentation |
| 3 | - **Triển khai hạ tầng Amplify Hosting:** <br>&emsp; + Kết nối kho lưu trữ mã nguồn Git của frontend với AWS Amplify Hosting <br>&emsp; + Thiết lập các biến môi trường (environment variables) và cấu hình các bước build tự động (CD pipeline) | 07/07/2026 | 07/07/2026 | AWS Amplify Console |
| 4 | - **Cấu hình Rewrite cho Client-Side Routing:** <br>&emsp; + Kiểm thử các đường dẫn React Router điều hướng trên môi trường Amplify (ví dụ: `/dang-nhap`, `/lop-hoc`, `/tai-khoan-cua-toi`) <br>&emsp; + Cấu hình quy tắc rewrite/redirect cho ứng dụng Single Page Application (SPA) nhằm khắc phục lỗi 404 khi reload trang | 08/07/2026 | 08/07/2026 | [AWS Amplify Redirects Guide](https://docs.aws.amazon.com/amplify/latest/userguide/redirects.html) |
| 5 | - **Cấu hình Route 53 và Ràng buộc CORS:** <br>&emsp; + Thực hiện trỏ tên miền (custom domain) thông qua hosted zone của AWS Route 53 <br>&emsp; + Cập nhật và tinh chỉnh cấu hình CORS tại API Gateway để hỗ trợ xử lý request an toàn từ local, Amplify domain và custom domain mới | 09/07/2026 | 09/07/2026 | AWS Route 53 / API Gateway |
| 6 | - **Hoàn thiện Tài liệu và Kiểm thử Toàn diện (E2E):** <br>&emsp; + Tiến hành chạy thử nghiệm end-to-end các luồng nghiệp vụ chính của hệ thống để đảm bảo tính ổn định <br>&emsp; + Rà soát, bổ sung dữ liệu kiểm thử và hoàn thiện toàn bộ file tài liệu proposal kèm báo cáo workshop kết thúc tiến độ | 10/07/2026 | 10/07/2026 | Markdown / Jira |

### Kết quả đạt được tuần 12:

* Ứng dụng frontend được triển khai chạy live thành công trên hạ tầng phân phối của AWS Amplify Hosting với độ ổn định cao.
* Cấu hình chính xác quy tắc rewrite trên Amplify, giúp hệ thống nhận diện tốt các route động của React Router và loại bỏ hoàn toàn lỗi 404 khi truy cập trực tiếp link.
* Thiết lập hệ thống CORS linh hoạt, hỗ trợ giao tiếp API thông suốt từ môi trường local test đến các domain production thực tế.
* Hoàn tất rà soát và kiểm thử lại toàn bộ các luồng tính năng cốt lõi, bảo chứng hệ thống vận hành đúng chuẩn theo mô hình Cloud Serverless mới.
* Hoàn thành việc cập nhật, đóng gói đồng bộ toàn bộ tài liệu báo cáo kỹ thuật bao gồm proposal dự án, kịch bản test và báo cáo workshop tổng kết.