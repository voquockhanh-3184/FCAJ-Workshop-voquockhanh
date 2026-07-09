---
title : "Tạo thêm Lambda (Import Word Processor)"
date : 2024-01-01 
weight : 6
chapter : false
pre : " <b> 5.7.6. </b> "
---

#### Mục tiêu:
Khởi tạo một Lambda Function độc lập tên là `examora-import-word-processor-dev` để thực hiện:
*   Nhận thông báo sự kiện (event) khi tệp tin `.docx` được tải lên S3.
*   Đọc tệp tin Word từ S3 Upload Bucket.
*   Trích xuất (parse) nội dung danh sách câu hỏi.
*   Lưu các câu hỏi đã parse vào cơ sở dữ liệu MongoDB Atlas.
*   Ghi nhật ký quá trình import vào CloudWatch Logs để giám sát.

*(Các bước tạo Lambda chi tiết vui lòng xem lại hướng dẫn ở mục 5.5)*.

---

#### Cấu hình S3 ObjectCreated Trigger:
Chúng ta cần thêm sự kiện kích hoạt (Trigger) cho S3 Upload Bucket để khi giảng viên upload file `.docx`, hàm Lambda `examora-import-word-processor-dev` sẽ tự động được chạy.

1. Các bước cấu hình Trigger:
   * Điều hướng tới bảng điều khiển dịch vụ **Amazon S3** -> Chọn tên Bucket đã tạo -> Chuyển qua tab **Properties** (Thuộc tính) -> Cuộn xuống mục **Event notifications** -> Bấm **Create event notification**.

   ![Event Notification S3](/images/5-Workshop/5.7-S3/5.7.6-create-import-word-processor/LambdaWord1.png)

   * Điền thông tin cấu hình sự kiện:
     * **Event name**: Đặt tên gợi nhớ (ví dụ: `ImportWordTrigger`).
     * **Prefix** (tùy chọn): Có thể nhập `imports/word/raw/` để chỉ kích hoạt khi file upload vào đúng thư mục này.
     * **Event types**: Tích chọn **All object create events** (Tất cả sự kiện tạo object).

   ![Cấu hình Event name](/images/5-Workshop/5.7-S3/5.7.6-create-import-word-processor/LambdaWord2.png)

   ![Chọn Event types](/images/5-Workshop/5.7-S3/5.7.6-create-import-word-processor/LambdaWord3.png)

   * Cuộn xuống phần **Destination** (Đích đến):
     * **Destination**: Chọn **Lambda function**.
     * **Lambda function**: Chọn đúng hàm `examora-import-word-processor-dev` đã tạo.
   * Nhấn **Save changes** để lưu lại cấu hình.

   ![Cấu hình Destination](/images/5-Workshop/5.7-S3/5.7.6-create-import-word-processor/LambdaWord4.png)

2. Xây dựng mã nguồn xử lý (Backend Logic):
   * Trong source code của Lambda Processor này, chúng ta cần triển khai các hàm xử lý chính sau:
     * `handler(event)`: Hàm Entrypoint nhận sự kiện `S3 ObjectCreated`.
     * `getS3ObjectBuffer(bucket, key)`: Đọc và lấy buffer dữ liệu file `.docx` từ S3.
     * `parseExamIdFromKey(key)`: Trích xuất thông tin ID bài thi (`examId`) từ đường dẫn tệp tin.
     * `parseQuestionsFromWord(buffer)`: Sử dụng thư viện `mammoth` để parse nội dung file Word thành dạng HTML/Raw text, sau đó trích xuất ra danh sách câu hỏi.
     * `normalizeQuestions(rawQuestions)`: Chuẩn hóa dữ liệu câu hỏi khớp với Schema cơ sở dữ liệu `BaiGiang.danhSachCauHoi`.
     * `saveQuestionsToMongo(examId, questions)`: Kết nối và lưu câu hỏi trực tiếp vào MongoDB Atlas.
     * `getMongoUriFromSecretsManager()`: Lấy chuỗi kết nối MongoDB URI bảo mật từ AWS Secrets Manager.
   * Thực hiện cài đặt các package phụ thuộc trong thư mục code của Lambda:
     ```bash
     npm install @aws-sdk/client-s3 @aws-sdk/client-secrets-manager mammoth mongodb
     ```
   * Đóng gói mã nguồn thành file `.zip` và tải lên hàm Lambda `examora-import-word-processor-dev` để hoàn tất triển khai.

   ![Deploy Lambda Import Word Processor](/images/5-Workshop/5.7-S3/5.7.6-create-import-word-processor/LambdaWord5.png)
