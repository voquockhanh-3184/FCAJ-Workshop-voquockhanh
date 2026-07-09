---
title : "Cấu hình SQS và Lambda Grading Worker"
date : 2024-01-01 
weight : 8 
chapter : false
pre : " <b> 5.8. </b> "
---

#### 5.8.1. Tổng quan:
Trong luồng *Exam Submission & Grading Pipeline*, Examora sử dụng **Amazon SQS Grading Queue** và **Lambda Grading Worker** để tách biệt quá trình chấm bài thi ra khỏi luồng xử lý request nộp bài chính của sinh viên (chấm bài bất đồng bộ). 

Khi sinh viên bấm nộp đáp án, Lambda Backend API sẽ không thực hiện chấm điểm trực tiếp ngay lập tức. Thay vào đó, API chỉ validate cấu trúc bài nộp, lưu attempt (lượt thi) ở trạng thái chờ chấm (`PENDING_GRADING`) và gửi một grading job (thông tin chấm bài) vào hàng đợi SQS. Sau đó, Lambda Grading Worker sẽ tự động được kích hoạt để đọc message từ hàng đợi SQS, kết nối tới cơ sở dữ liệu MongoDB Atlas để chấm điểm và cập nhật kết quả.

![Pipeline chấm thi bất đồng bộ](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.1-overview/SQS1.png)

#### Nội dung:
1. [Tạo SQS Grading Queue](5.8.2-create-sqs-queue/)
2. [Tạo Lambda Grading Worker](5.8.3-create-lambda-grading-worker/)
3. [Kiểm thử hoạt động SQS và Lambda Grading Worker](5.8.4-test-grading-pipeline/)
