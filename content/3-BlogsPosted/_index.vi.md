---
title: "Các bài blogs đã đăng"
date: 2026-07-05
weight: 3
chapter: false
pre: " <b> 3. </b> "
---


Tại đây sẽ là phần liệt kê, giới thiệu các blogs mà nhóm mình đã đăng trên [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj). Ví dụ:

###  [Blog 1 - Tự động hóa Refresh Dữ liệu giữa các Tài khoản AWS cho Amazon RDS Multi-AZ DB Cluster](3.1-Blog1/)
Blog này giới thiệu giải pháp tự động hóa việc refresh dữ liệu giữa các tài khoản AWS cho Amazon RDS Multi-AZ DB Cluster. Thông qua việc kết hợp AWS Lambda, AWS Step Functions, Amazon EventBridge và AWS KMS, bài viết hướng dẫn xây dựng một pipeline serverless giúp đồng bộ dữ liệu từ môi trường production sang staging hoặc testing một cách tự động, giảm thao tác thủ công, hạn chế sai sót và đảm bảo dữ liệu luôn được bảo mật trong quá trình chia sẻ giữa các tài khoản AWS.

###  [Blog 2 - Tìm hiểu Amazon Aurora DSQL – Giải pháp cơ sở dữ liệu mới trên AWS](3.2-Blog2/)
Blog này giới thiệu Amazon Aurora DSQL, dịch vụ cơ sở dữ liệu SQL phân tán theo mô hình serverless do AWS phát triển. Bài viết trình bày các đặc điểm nổi bật như khả năng tự động mở rộng mà không cần sharding, kiến trúc Active-Active giúp tăng tính sẵn sàng, khả năng tương thích với PostgreSQL và việc không cần quản lý hạ tầng. Đây là một giải pháp phù hợp cho các ứng dụng hiện đại cần khả năng mở rộng linh hoạt, hiệu năng cao và giảm chi phí vận hành.

###  [Blog 3 - Tối ưu chi phí EC2 bằng cách phân tích Capacity Reservations với Amazon Athena](3.3-Blog3/)
Blog này giới thiệu giải pháp tối ưu chi phí Amazon EC2 On-Demand Capacity Reservations (ODCR) bằng cách kết hợp EC2 Capacity Manager, Amazon S3 và Amazon Athena. Bài viết hướng dẫn cách lưu trữ dữ liệu sử dụng capacity theo thời gian dài, truy vấn trực tiếp bằng SQL và phân tích mức độ sử dụng reservation để phát hiện các tài nguyên đang gây lãng phí. Giải pháp giúp doanh nghiệp chủ động theo dõi, đánh giá và tối ưu chi phí EC2 dựa trên dữ liệu thực tế thay vì chỉ dựa vào báo cáo trên AWS Console.