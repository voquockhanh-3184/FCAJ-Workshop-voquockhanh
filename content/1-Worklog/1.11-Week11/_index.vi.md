---
title: "Worklog Tuần 11"
date: 2026-07-06
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---


### Mục tiêu tuần 11:

* Tách biệt logic chấm điểm bài thi khỏi luồng xử lý request nộp bài bằng cách sử dụng SQS Grading Queue và một Lambda Grading Worker.
* Thiết lập kiến trúc bất đồng bộ, hướng sự kiện (event-driven) nhằm tối ưu hóa quá trình xử lý nộp bài và chịu tải tốt khi có lượng truy cập đồng thời cao (high concurrency).

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Công cụ / Nền tảng |
| --- | --- | --- | --- | --- |
| 2 | - **Cấu hình SQS Queue:** <br>&emsp; + Khởi tạo và cấu hình hàng đợi Amazon SQS Grading Queue <br>&emsp; + Thiết lập hàng đợi tin nhắn lỗi (Dead-Letter Queue - DLQ) và các chính sách thử lại (retry policies) cho các tác vụ chấm điểm thất bại | 29/06/2026 | 29/06/2026 | AWS Management Console |
| 3 | - **Tối ưu luồng xử lý nộp bài (Refactor):** <br>&emsp; + Cấu trúc lại backend để khi nhận request nộp bài sẽ lập tức lưu trạng thái là "grading" <br>&emsp; + Triển khai logic gửi payload (tin nhắn) chứa thông tin bài thi vào hàng đợi SQS | 30/06/2026 | 30/06/2026 | AWS SDK / Node.js |
| 4 | - **Kiểm thử tích hợp Frontend và SQS:** <br>&emsp; + Thử nghiệm các lượt nộp bài thi được kích hoạt từ giao diện phía client <br>&emsp; + Xác thực trạng thái khởi tạo "grading" cập nhật đúng trong MongoDB và kiểm tra cấu trúc dữ liệu tin nhắn gửi đến SQS | 01/07/2026 | 01/07/2026 | [Amazon SQS Developer Guide](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-basic-architecture.html) |
| 5 | - **Phát triển Lambda Grading Worker:** <br>&emsp; + Xây dựng một hàm Lambda độc lập (Worker) được kích hoạt tự động bởi sự kiện từ SQS <br>&emsp; + Viết logic xử lý chấm điểm: tính toán số điểm, thống kê số câu đúng/sai, và định dạng chi tiết đáp án lựa chọn | 02/07/2026 | 02/07/2026 | AWS Lambda |
| 6 | - **Kiểm tra kết quả Worker và Xác thực MongoDB:** <br>&emsp; + Giám sát và xác minh dữ liệu đầu ra sau khi hàm Lambda Worker thực hiện chấm điểm xong <br>&emsp; + Đảm bảo các chỉ số điểm, số câu đúng/sai và phân tích chi tiết lựa chọn của thí sinh được lưu trữ chính xác vào cơ sở dữ liệu | 03/07/2026 | 03/07/2026 | MongoDB Compass |

### Kết quả đạt được tuần 11:

* Tách biệt thành công tác vụ chấm điểm nặng nề ra khỏi luồng request chính của người dùng, giúp giảm thiểu tối đa thời gian phản hồi (latency) của API nộp bài.
* Cấu hình hoàn chỉnh hạ tầng Amazon SQS Grading Queue, đóng vai trò như một bộ đệm đáng tin cậy để xử lý mượt mà lượng lớn bài nộp cùng lúc.
* Phát triển và triển khai thành công AWS Lambda Grading Worker giúp bóc tách dữ liệu bất đồng bộ và tự động cập nhật kết quả thi độc lập.
* Kiểm thử thông suốt quy trình end-to-end từ lúc nộp bài, trạng thái chuyển dịch linh hoạt từ "grading" sang sơ đồ dữ liệu đã được chấm điểm hoàn tất trong MongoDB Compass.