---
title : "Dọn dẹp tài nguyên"
date : 2024-01-01 
weight : 10 
chapter : false
pre : " <b> 5.10. </b> "
---

Sau khi hoàn thành bài thực hành và kiểm thử hệ thống Examora thành công, chúng ta tiến hành xóa các tài nguyên AWS đã khởi tạo nhằm tối ưu hóa chi phí và tránh phát sinh hóa đơn không mong muốn.

---

#### 1. Xóa AWS Amplify Hosting
*   **Gỡ bỏ Custom Domain:**
    *   Truy cập dịch vụ **AWS Amplify** -> Chọn ứng dụng Frontend của bạn.
    *   Ở menu bên trái, chọn **Custom domains** -> Chọn domain của bạn -> Chọn **Actions** -> Chọn **Delete** (Xác nhận và xóa).

    ![Gỡ Custom Domain khỏi Amplify](/images/5-Workshop/5.10-Don-dep-tai-nguyen/GoDomain1.png)

*   **Xóa Amplify App:**
    *   Quay lại trang cấu hình App của bạn -> Vào mục **App settings** ở menu trái -> Chọn **Delete app** ở bên phải -> Nhập xác nhận và chọn **Delete** để xóa ứng dụng Frontend.

    ![Xóa Amplify App](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaAmplify.png)

---

#### 2. Xóa Amazon Route 53
*   **Xóa các bản ghi (Records):**
    *   Truy cập **Route 53** -> Chọn **Hosted zones** -> Click chọn tên miền của bạn.
    *   Tích chọn tất cả các bản ghi tự tạo (như bản ghi loại A, CNAME,...), **giữ lại bản ghi NS và SOA mặc định** -> Nhấn **Delete record** để xóa.

    ![Xóa các bản ghi DNS](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaRecord.png)

*   **Xóa Hosted Zone:**
    *   Sau khi Hosted zone chỉ còn lại 2 bản ghi mặc định (NS và SOA) -> Quay lại danh sách Hosted zones -> Tích chọn Hosted zone của bạn -> Nhấn **Delete hosted zone** -> Nhập xác nhận và xóa.

    ![Xóa Hosted Zone](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaHostedzones.png)

---

#### 3. Xóa Amazon API Gateway
*   Truy cập **API Gateway** -> Chọn mục **APIs** ở menu trái -> Chọn API đã tạo (ví dụ: `examora-api`).
*   Nhấn nút **Delete** ở góc phải -> Nhập chữ xác nhận (tên API) để xóa hoàn toàn API Gateway.

    ![Xóa API Gateway](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaAPIGateway.png)

---

#### 4. Gỡ bỏ Trigger trước khi xóa Lambda
*   **Gỡ bỏ S3 trigger của Lambda Import Word Processor:**
    *   Truy cập hàm `examora-import-word-processor-dev` -> Tại giao diện Function overview, tích chọn trigger **S3** -> Nhấn **Remove** (hoặc **Delete**) để gỡ bỏ.

    ![Xóa S3 Trigger khỏi Lambda](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaS3Trigger.png)

*   **Gỡ bỏ SQS trigger của Lambda Grading Worker:**
    *   Tương tự như trên, truy cập hàm `examora-grading-worker-dev` -> Chọn trigger **SQS** -> Nhấn **Remove** để gỡ bỏ trigger kết nối với hàng đợi.

    ![Xóa SQS Trigger khỏi Lambda](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaS3SQS.png)

---

#### 5. Xóa Lambda Functions
*   Truy cập **Lambda** -> Mục **Functions** -> Tích chọn các hàm Lambda đã khởi tạo cho dự án:
    *   `examora-backend-api-dev`
    *   `examora-import-word-processor-dev`
    *   `examora-grading-worker-dev`
*   Chọn **Actions** -> Chọn **Delete** -> Xác nhận xóa các Function.

    ![Xóa các Lambda Functions](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaLambda.png)

---

#### 6. Xóa Amazon SQS Queue và Dead-letter Queue (DLQ)
*   Truy cập **Amazon SQS** -> Mục **Queues**.
*   Chọn lần lượt hoặc chọn đồng thời các queue đã tạo cho dự án:
    *   `examora-grading-queue-dev`
    *   `examora-grading-dlq-dev`
*   Nhấn **Delete** -> Nhập dòng chữ xác nhận và chọn **Delete** để xóa hoàn toàn các hàng đợi.

    ![Xóa SQS Queues](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaSQS.png)

---

#### 7. Xóa Amazon S3 Buckets
*   Truy cập **Amazon S3** -> Chọn **Buckets**.
*   Do S3 chỉ cho phép xóa bucket trống, bạn cần dọn sạch file trước:
    *   Chọn bucket của bạn -> Chọn **Empty** -> Nhập dòng chữ xác nhận để dọn sạch toàn bộ các file đã upload.
    *   Quay lại danh sách Buckets -> Chọn bucket -> Nhấn **Delete** -> Nhập xác nhận để xóa hoàn toàn bucket.
    *   Thực hiện tương tự cho cả bucket upload và các bucket khác đã tạo.

    ![Xóa S3 Buckets](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaBuckets.png)

---

#### 8. Xóa Amazon Cognito User Pool
*   Truy cập dịch vụ **Amazon Cognito** -> Chọn **User pools**.
*   Tích chọn User pool của dự án -> Nhấn **Delete** -> Nhập dòng chữ xác nhận để xóa toàn bộ thông tin người dùng và nhóm.

    ![Xóa Cognito User Pool](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaCognito.png)

---

#### 9. Xóa Amazon SES Identity
*   Truy cập dịch vụ **Amazon SES** -> Ở menu trái chọn **Configuration** -> Chọn **Identities**.
*   Tích chọn Email identity mà bạn đã xác thực cho dự án -> Nhấn **Delete** -> Xác nhận xóa.

    ![Xóa SES Email Identity](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaSES.png)

---

#### 10. Xóa AWS Secrets Manager Secret
*   Truy cập **Secrets Manager** -> Mục **Secrets** -> Chọn Secret lưu trữ MongoDB URI đã tạo.
*   Chọn **Actions** -> Chọn **Delete secret**.
*   Chọn thời gian khôi phục (recovery window) tối thiểu (ví dụ: `7 days`) -> Chọn **Schedule deletion** để lên lịch xóa.

    ![Xóa Secret trong Secrets Manager](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaSecret.png)

---

#### 11. Xóa Amazon CloudWatch Log Groups
*   Truy cập **CloudWatch** -> Menu trái chọn **Log groups** dưới mục **Logs**.
*   Tích chọn các log group của các hàm Lambda dự án đã tạo -> Chọn **Actions** -> Chọn **Delete log group(s)** -> Xác nhận xóa để giải phóng dung lượng log lưu trữ.

    ![Xóa các Log Groups](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaCloudWatch.png)

---

#### 12. Xóa IAM Roles và Inline Policies
*   **Lưu ý:** Chỉ xóa các Role được tạo riêng phục vụ cho dự án Examora.
*   Truy cập dịch vụ **IAM** -> Chọn **Roles** ở menu trái.
*   Tìm kiếm và tích chọn các IAM execution role đã tạo cho các Lambda API, Lambda Processor và Lambda Grading Worker.
*   Nhấn nút **Delete** -> Nhập chữ xác nhận và nhấn **Delete** để xóa các role và chính sách bảo mật đi kèm.

    ![Xóa các dự án IAM Roles](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaIAMRole.png)
