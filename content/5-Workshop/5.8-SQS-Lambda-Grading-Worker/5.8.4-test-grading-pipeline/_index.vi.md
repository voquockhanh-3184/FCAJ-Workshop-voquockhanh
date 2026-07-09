---
title : "Kiểm thử SQS và Lambda Grading Worker"
date : 2024-01-01 
weight : 4
chapter : false
pre : " <b> 5.8.4. </b> "
---

#### Các bước thực hiện:

1. Chạy web local và làm bài thi:
   * Khởi chạy ứng dụng Frontend local -> Đăng nhập bằng tài khoản sinh viên.
   * Truy cập vào danh sách đề thi -> Chọn thi thử một đề bất kỳ -> Tiến hành chọn đáp án cho các câu hỏi.

   ![Sinh viên làm bài thi thử](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.4-test-grading-pipeline/TestSQS1.png)

2. Nộp bài và đợi kết quả:
   * Sau khi chọn xong đáp án -> Nhấn **Nộp bài**.
   * Hệ thống sẽ hiển thị thông báo gửi thông tin nộp bài thành công và đang đợi kết quả chấm điểm. 
   * Do Backend API phản hồi `202 Accepted` và đưa bài thi vào hàng đợi SQS, Lambda Grading Worker sẽ xử lý bất đồng bộ trong nền và tự động trả về điểm số sau vài giây mà không cần sinh viên phải tải lại trang.

   ![Nộp bài thi thành công](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.4-test-grading-pipeline/TestSQS2.png)

   ![Điểm số hiển thị sau khi chấm xong](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.4-test-grading-pipeline/TestSQS3.png)

3. Kiểm tra nhật ký thực thi trên Amazon CloudWatch:
   * Truy cập CloudWatch Logs của Lambda function `examora-grading-worker-dev` -> Kiểm tra các Log Stream.
   * Kết quả cho thấy worker khởi chạy bình thường, nhận sự kiện từ SQS, giải mã payload và thực hiện chấm bài thành công.

   ![Nhật ký thực thi CloudWatch Logs](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.4-test-grading-pipeline/TestSQS4.png)

#### Kết luận:
Hệ thống đã hoàn thành việc triển khai luồng chấm bài bất đồng bộ bằng **Amazon SQS** và **Lambda Grading Worker**. Điều này giúp Backend API chỉ tập trung tiếp nhận các lượt nộp bài một cách nhanh chóng, tránh tình trạng nghẽn kết nối hoặc quá tải khi có lượng lớn sinh viên nộp bài thi cùng lúc.
