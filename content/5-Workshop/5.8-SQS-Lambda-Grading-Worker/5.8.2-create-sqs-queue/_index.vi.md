---
title : "Tạo SQS Grading Queue"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.8.2. </b> "
---

Để triển khai hệ thống hàng đợi, chúng ta cần tạo hai hàng đợi SQS: một hàng đợi chính (`examora-grading-queue-dev`) và một hàng đợi tin nhắn lỗi (**Dead-letter Queue - DLQ**) để chứa các bản tin xử lý lỗi nhiều lần giúp debug.

#### Các bước thực hiện:

1. Tạo Dead-letter Queue (DLQ):
   * Truy cập bảng điều khiển dịch vụ **Amazon SQS** -> Chọn **Queues** -> Nhấn **Create queue**.
   * Cấu hình hàng đợi DLQ:
     * **Type**: Chọn `Standard`.
     * **Name**: Nhập `examora-grading-dlq-dev`.
     * Các thông số cấu hình khác giữ nguyên mặc định -> Nhấn **Create queue**.

   ![Cấu hình tạo DLQ](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.2-create-sqs-queue/SQS2.png)

   ![Tạo DLQ thành công](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.2-create-sqs-queue/SQS3.png)

2. Tạo SQS Grading Queue (Hàng đợi chính):
   * Nhấn **Create queue** lần nữa để tạo hàng đợi chính.
   * Cấu hình hàng đợi chính:
     * **Type**: Chọn `Standard`.
     * **Name**: Nhập `examora-grading-queue-dev`.
     * Kéo xuống mục **Dead-letter queue** -> Chọn **Enabled**.
     * **Choose queue**: Chọn đúng hàng đợi DLQ vừa tạo ở bước trên (`examora-grading-dlq-dev`).
     * **Maximum receives**: Điền `3` (tin nhắn xử lý lỗi quá 3 lần sẽ chuyển vào DLQ).
   * Nhấn **Create queue** để hoàn tất.

   ![Tạo SQS Grading Queue với DLQ](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.2-create-sqs-queue/SQS4.png)

3. Lưu lại Queue URL và ARN:
   * Sau khi tạo xong, mở chi tiết hàng đợi chính để lưu lại hai giá trị:
     * **Queue URL** (ví dụ: `https://sqs.ap-southeast-1.amazonaws.com/<ACCOUNT_ID>/examora-grading-queue-dev`)
     * **Queue ARN** (ví dụ: `arn:aws:sqs:ap-southeast-1:<ACCOUNT_ID>:examora-grading-queue-dev`)

4. Gắn quyền gửi tin nhắn SQS cho Lambda Backend API:
   * Do Lambda Backend cần gửi thông tin chấm thi vào SQS, chúng ta cần bổ sung quyền `sqs:SendMessage` vào IAM execution role của nó.
   * Quay lại IAM Role của Lambda Backend API -> Chọn tab **Permissions** -> Thêm **Inline policy** bằng JSON:

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "SendGradingJobToSQS",
         "Effect": "Allow",
         "Action": [
           "sqs:SendMessage"
         ],
         "Resource": "arn:aws:sqs:ap-southeast-1:<ACCOUNT_ID>:examora-grading-queue-dev"
       }
     ]
   }
   ```
   *(Đổi `<ACCOUNT_ID>` thành ID tài khoản AWS của bạn)*.
   * Đặt tên cho policy là: `examora-backend-send-grading-policy-dev`.

   ![Thêm quyền SendMessage SQS](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.2-create-sqs-queue/SQS5.png)

5. Bổ sung cấu hình môi trường cho Lambda Backend API:
   * Vào Lambda Backend API -> Tab **Configuration** -> **Environment variables** -> Bấm **Edit** và thêm biến môi trường sau:
     * `GRADING_QUEUE_URL` = `<Queue URL của bạn>`
   * Bấm **Save** để lưu cấu hình.

   ![Khai báo Queue URL làm biến môi trường](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.2-create-sqs-queue/SQS6.png)
