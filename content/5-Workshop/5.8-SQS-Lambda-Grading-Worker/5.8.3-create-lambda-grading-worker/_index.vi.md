---
title : "Tạo Lambda Grading Worker"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.8.3. </b> "
---

#### Các bước thực hiện:

1. Tạo IAM Execution Role cho Grading Worker:
   * Đặt tên Role: `examora-grading-worker-lambda-role-dev`.
   * Thêm **Inline policy** cho phép đọc thông điệp từ SQS và đọc mật khẩu kết nối DB từ Secrets Manager:

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "ReadGradingQueueMessages",
         "Effect": "Allow",
         "Action": [
           "sqs:ReceiveMessage",
           "sqs:DeleteMessage",
           "sqs:GetQueueAttributes",
           "sqs:ChangeMessageVisibility"
         ],
         "Resource": "arn:aws:sqs:ap-southeast-1:<ACCOUNT_ID>:examora-grading-queue-dev"
       },
       {
         "Sid": "ReadMongoDBSecret",
         "Effect": "Allow",
         "Action": [
           "secretsmanager:GetSecretValue"
         ],
         "Resource": "arn:aws:secretsmanager:ap-southeast-1:<ACCOUNT_ID>:secret:/examora/dev/mongodb-*"
       }
     ]
   }
   ```
   *(Thay `<ACCOUNT_ID>` bằng ID tài khoản AWS của bạn)*.

   ![Gắn Policy IAM cho Grading Worker](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.3-create-lambda-grading-worker/LambdaGrandWork1.png)

2. Tạo Function Lambda Grading Worker:
   * Tên function: `examora-grading-worker-dev`.
   * **Runtime**: Chọn `Node.js 22.x` (đồng bộ với Lambda Backend).
   * **Role**: Chọn execution role vừa tạo ở bước trên (`examora-grading-worker-lambda-role-dev`).

   ![Khởi tạo Lambda function](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.3-create-lambda-grading-worker/LambdaGrandWork2.png)

3. Gắn SQS Trigger cho Lambda Grading Worker:
   * Trên trang chi tiết hàm `examora-grading-worker-dev` -> Bấm **Add trigger**.
   * Tìm chọn trigger **SQS** -> Tại ô **SQS queue**, chọn đúng hàng đợi `examora-grading-queue-dev`.
   * Nhấn **Add** để lưu lại.

   ![Cấu hình SQS Trigger](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.3-create-lambda-grading-worker/SQSTrigger1.png)

   ![Gắn Trigger SQS thành công](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.3-create-lambda-grading-worker/SQSTrigger2.png)

4. Cập nhật mã nguồn hệ thống:
   * **Phía Backend API (Gửi grading job):** Cập nhật luồng nộp bài của sinh viên như sau:
     * Xác thực JWT.
     * Kiểm tra user là `STUDENT`.
     * Kiểm tra quyền làm bài.
     * Lưu attempt vào MongoDB với trạng thái `PENDING_GRADING`.
     * Gửi grading job vào SQS với cấu trúc Payload:
       ```json
       {
         "attemptId": "<attemptId>",
         "examId": "<examId>",
         "studentId": "<studentId>",
         "submittedAt": "2026-07-06T10:00:00.000Z"
       }
       ```
     * Trả về mã phản hồi `202 Accepted` cho frontend để giảm thời gian chờ đợi của user.

   * **Phía Lambda Grading Worker (Xử lý chấm bài):** Triển khai code logic:
     * Nhận SQS event.
     * Parse từng bản ghi trong `event.Records`.
     * Trích xuất `attemptId`, `examId`, `studentId` từ body của message.
     * Kết nối database MongoDB Atlas bằng URI đọc từ Secrets Manager.
     * Lấy dữ liệu bài thi (đáp án) và các câu hỏi tương ứng.
     * Tính toán số câu trả lời đúng, sai và quy đổi điểm số.
     * Lưu kết quả chấm điểm vào MongoDB.
     * Cập nhật trạng thái attempt thành `GRADED`.

   * **Triển khai mã nguồn:**
     * Nén mã nguồn Backend thành file `.zip` và tải lên hàm Lambda tương ứng.
     * Đối với Lambda Grading Worker, cấu hình **Handler** là: **`src/lambdas/gradingWorker/handler.handler`**.
