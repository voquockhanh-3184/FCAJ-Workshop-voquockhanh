---
title : "Tạo secret trong AWS Secrets Manager"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.3.2. </b> "
---

#### Tóm tắt:
*   Chúng ta sử dụng AWS Secrets Manager để lưu trữ thông tin kết nối MongoDB Atlas của dự án Examora.
*   Thay vì ghi cứng `MONGO_URI` trong mã nguồn hoặc tệp cấu hình, backend Lambda sẽ đọc secret `/examora/dev/mongodb` khi khởi tạo.
*   Secret này sẽ chứa 2 cặp khóa-giá trị: `MONGO_URI` và `MONGO_DB_NAME`.
*   Ở môi trường workshop/dev, chúng ta sẽ tắt tính năng tự động xoay vòng (automatic rotation) để đơn giản hóa quá trình triển khai. Trong môi trường production, secret nên được rotate định kỳ và kiểm soát quyền truy cập chặt chẽ bằng chính sách đặc quyền tối thiểu (IAM least privilege).

#### Các bước thực hiện:

1. Trên thanh tìm kiếm của AWS Console, nhập **Secrets Manager** -> Chọn **Secrets Manager** từ kết quả tìm kiếm -> Bấm chọn **Store a new secret**.

![Secrets Manager Console](/images/5-Workshop/5.3-AWS-Secret-Manager/5.3.2-create-secret/SecretManage5.1.png)

2. Khởi tạo secret mới:
- Tại mục **Choose secret type** -> Chọn **Other type of secret**.
- Nhập các giá trị **Key/value** cho secret (thêm 2 cặp key/value tương ứng):
  - Key: `MONGO_URI` | Value: `<chuỗi kết nối MongoDB Atlas của bạn>`
  - Key: `MONGO_DB_NAME` | Value: `WebsiteTest2026`
- Tại phần **Encryption key**, giữ nguyên tùy chọn mặc định (`aws/secretsmanager`).
- Bấm **Next**.

![Choose Secret Type](/images/5-Workshop/5.3-AWS-Secret-Manager/5.3.2-create-secret/SecretManage5.2.png)

3. Nhập tên cho secret (ví dụ: `/examora/dev/mongodb`) -> Bấm **Next**.

![Secret Name](/images/5-Workshop/5.3-AWS-Secret-Manager/5.3.2-create-secret/SecretManage5.3.png)

4. Cấu hình xoay vòng secret trong mục **Configure rotation** -> Chọn **Disable automatic rotation**.
- Kiểm tra lại toàn bộ thông tin cấu hình một lần nữa -> Nhấn **Store** ở góc dưới cùng để tạo secret.

![Configure Rotation](/images/5-Workshop/5.3-AWS-Secret-Manager/5.3.2-create-secret/SecretManage5.4.png)

5. Secret đã được tạo thành công:

![Secret Created Successfully](/images/5-Workshop/5.3-AWS-Secret-Manager/5.3.2-create-secret/SecretManage5.5.png)

*   Sau khi tạo thành công secret `/examora/dev/mongodb`, bạn hãy ghi lại **Secret ARN** để sử dụng trong bước tạo Lambda execution role tiếp theo.
*   Các hàm Lambda cần kết nối tới MongoDB Atlas sẽ được cấp quyền `secretsmanager:GetSecretValue` trên secret này.
*   Phần cấu hình quyền IAM cụ thể cho Lambda đọc secret sẽ được thực hiện chi tiết ở bước tạo Lambda Backend API.
