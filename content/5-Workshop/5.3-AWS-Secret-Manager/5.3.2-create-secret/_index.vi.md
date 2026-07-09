---
title : "Tạo Secret trong AWS Secrets Manager"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.3.2. </b> "
---

#### Tóm tắt:
*   Chúng ta sử dụng AWS Secrets Manager để lưu trữ thông tin kết nối MongoDB Atlas cho dự án Examora.
*   Thay vì viết cứng (hardcode) chuỗi `MONGO_URI` trong mã nguồn hoặc tệp cấu hình, các hàm Lambda ở backend sẽ truy xuất động secret `/examora/dev/mongodb` này khi khởi tạo.
*   Secret chứa hai cặp key-value: `MONGO_URI` và `MONGO_DB_NAME`.
*   Trong môi trường workshop/dev, tính năng tự động xoay vòng mã khóa (automatic rotation) được tắt để đơn giản hóa quá trình triển khai. Trên môi trường thực tế (production), các secret cần được xoay vòng định kỳ và kiểm soát truy cập nghiêm ngặt theo nguyên tắc đặc quyền tối thiểu của IAM.

#### Hướng dẫn từng bước thực hiện:

1. Tại thanh tìm kiếm của AWS Console, nhập **Secrets Manager** -> Chọn **Secrets Manager** -> Nhấn chọn **Store a new secret**.

![Secrets Manager Console](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.3-AWS-Secret-Manager/5.3.2-create-secret/SecretManage5.1.png)

2. Tạo một secret mới:
- Tại mục **Choose secret type** -> Chọn **Other type of secret**.
- Nhập các giá trị **Key/value** cho secret (thêm 2 cặp key/value):
  - Key: `MONGO_URI` | Value: `<chuỗi kết nối MongoDB Atlas của bạn>`
  - Key: `MONGO_DB_NAME` | Value: `WebsiteTest2026`
- Tại mục **Encryption key**, giữ nguyên khóa mã hóa mặc định (`aws/secretsmanager`).
- Nhấn **Next**.

![Chọn loại Secret](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.3-AWS-Secret-Manager/5.3.2-create-secret/SecretManage5.2.png)

3. Thiết lập tên định danh cho secret (Ví dụ: `/examora/dev/mongodb`) -> Nhấn **Next**.

![Đặt tên Secret](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.3-AWS-Secret-Manager/5.3.2-create-secret/SecretManage5.3.png)

4. Tại phần cấu hình xoay vòng mã khóa **Configure rotation** -> Tích chọn tắt **Automatic rotation**.
- Xem lại toàn bộ thông tin cấu hình chi tiết -> Nhấn chọn **Store** ở góc dưới cùng để chính thức tạo secret.

![Cấu hình xoay vòng mã](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.3-AWS-Secret-Manager/5.3.2-create-secret/SecretManage5.4.png)

5. Secret đã được tạo thành công:

![Tạo Secret thành công](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.3-AWS-Secret-Manager/5.3.2-create-secret/SecretManage5.5.png)

*   Sau khi tạo xong secret `/examora/dev/mongodb`, bạn hãy lưu lại mã **Secret ARN** để sử dụng cho bước tạo Lambda execution role tiếp theo.
*   Các hàm Lambda cần truy cập cơ sở dữ liệu sẽ được cấp quyền `secretsmanager:GetSecretValue` trên chính tài nguyên secret này.
*   Việc gán chính sách IAM policy cụ thể cho phép Lambda đọc secret sẽ được cấu hình chi tiết trong bước tạo Lambda Backend API.