---
title : "Tạo người dùng IAM và bật mã xác thực MFA"
date : 2026-07-09 
weight : 4
chapter : false
pre : " <b> 5.2.4. </b> "
---

1. Tại giao diện **IAM Dashboard** (menu bên trái), chọn mục **Users** -> Nhấn chọn **Create user** để bắt đầu quy trình tạo một IAM User:

![Tạo Người Dùng](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.1.png)

2. Cấu hình các thông tin chi tiết cần thiết cho người dùng:

- **Bước 1**: Nhập tên người dùng (username) cho IAM User:

![Đặt Tên Người Dùng](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.2.png)

- **Bước 2**: Thêm người dùng vào nhóm `ExamoraAdminGroup` đã tạo trước đó để gán các quyền quản trị:

![Thêm Người Dùng Vào Nhóm](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.3.png)

- **Bước 3**: Xem lại toàn bộ thông tin chi tiết của người dùng và nhấn **Create user** để hoàn tất:

![Xem lại và Tạo](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.4.png)

- Tương tự, tiến hành tạo các IAM user khác cho các thành viên còn lại trong nhóm nhưng với các quyền hạn thấp hơn, phù hợp với vai trò của từng người.
- Việc áp dụng nguyên tắc đặc quyền tối thiểu (Least privilege access) giúp quản lý phân quyền rõ ràng, đồng thời giảm thiểu rủi ro từ việc chia sẻ chung tài khoản Root hoặc dùng chung một IAM user duy nhất.

![Danh sách IAM User](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.5.png)

3. Bật mã xác thực đa yếu tố MFA (Multi-Factor Authentication) cho người dùng IAM để tăng cường bảo mật khi đăng nhập vào AWS Console:

{{% notice note %}}
Đối với access key, chỉ nên tạo cho những người dùng thực sự cần sử dụng AWS CLI hoặc SAM để triển khai/dọn dẹp tài nguyên. Không tạo quyền access key này một cách đại trà cho tất cả thành viên.
{{% /notice %}}

- Nhấp chọn vào user cần cấu hình MFA, sau đó chuyển sang tab **Security credentials**.
- Tại khu vực **Multi-factor authentication (MFA)**, nhấn chọn **Assign MFA device**:

![Gán Thiết Bị MFA](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.6.png)

- Đặt tên định danh cho thiết bị MFA và lựa chọn phương thức xác thực mong muốn:

![Thiết Lập Thiết Bị MFA](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.7.png)