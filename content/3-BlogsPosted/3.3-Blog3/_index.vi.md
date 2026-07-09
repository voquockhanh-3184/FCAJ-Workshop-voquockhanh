---
title: "Blog 3"
date: 2026-07-05
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Tối ưu chi phí EC2 bằng cách phân tích Capacity Reservations với Amazon Athena

Việc tối ưu chi phí Amazon EC2 On-Demand Capacity Reservations (ODCR) giúp doanh nghiệp phát hiện và giảm thiểu các reservation không được sử dụng hiệu quả, từ đó tránh lãng phí chi phí khi vận hành hạ tầng AWS ở quy mô lớn. Giải pháp kết hợp EC2 Capacity Manager, Amazon S3 và Amazon Athena để lưu trữ, truy vấn và phân tích dữ liệu lịch sử dài hạn, giúp theo dõi xu hướng sử dụng capacity, hỗ trợ đưa ra quyết định tối ưu tài nguyên dựa trên dữ liệu thực tế thay vì chỉ dựa vào thông tin giới hạn trên AWS Console.

Các điểm chính cần nắm:

* Mục tiêu của giải pháp là phân tích và tối ưu chi phí Amazon EC2 On-Demand Capacity Reservations (ODCR) dựa trên dữ liệu lịch sử dài hạn, giúp phát hiện các reservation sử dụng không hiệu quả.
* On-Demand Capacity Reservations (ODCR) vẫn bị tính phí ngay cả khi không có EC2 instance sử dụng, dẫn đến lãng phí nếu reservation bị bỏ trống hoặc sử dụng dưới công suất.
* AWS Management Console chỉ lưu và hiển thị dữ liệu sử dụng Capacity Reservations trong 90 ngày, gây khó khăn khi phân tích xu hướng hoặc đánh giá hiệu quả sử dụng trong thời gian dài.
* EC2 Capacity Manager cho phép export dữ liệu sử dụng capacity theo giờ sang Amazon S3 dưới định dạng Parquet, phù hợp cho lưu trữ và phân tích dữ liệu quy mô lớn.
* Amazon Athena có thể truy vấn trực tiếp dữ liệu trên S3 bằng SQL, không cần xây dựng quy trình ETL hoặc triển khai data warehouse riêng.
* Giải pháp sử dụng Partition Projection của Athena để tự động nhận diện các partition mới, giúp dữ liệu được cập nhật liên tục mà không cần chạy lệnh cập nhật metadata thủ công.
* Giải pháp phù hợp với các doanh nghiệp quản lý nhiều AWS accounts và nhiều Region, giúp theo dõi và tối ưu chi phí EC2 dựa trên dữ liệu lịch sử thay vì chỉ dựa vào hóa đơn cuối tháng.
* Có thể mở rộng hệ thống bằng cách tích hợp với Amazon EventBridge Scheduler để tự động export và refresh dữ liệu định kỳ, hoặc kết hợp với Amazon QuickSight để xây dựng dashboard trực quan phục vụ giám sát và phân tích chi phí.

Giải pháp giúp doanh nghiệp chủ động phát hiện các Capacity Reservations sử dụng kém hiệu quả, từ đó điều chỉnh hoặc hủy các reservation không cần thiết để giảm chi phí. Việc lưu trữ dữ liệu dài hạn trên Amazon S3 và phân tích bằng Amazon Athena cũng tạo nền tảng cho các báo cáo và dashboard quản lý chi phí AWS ở quy mô lớn.

![Ảnh blog 3](/images/blog3.png)

[Link blog](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2204187187012908/#)

![Cấu trúc](/images/instructionblog3.png)