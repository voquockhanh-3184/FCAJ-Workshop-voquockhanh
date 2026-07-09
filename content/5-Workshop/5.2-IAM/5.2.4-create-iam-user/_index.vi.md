---
title : "Tạo IAM User và bật MFA"
date : 2024-01-01 
weight : 4
chapter : false
pre : " <b> 5.2.4. </b> "
---

1. Trong **IAM Dashboard** (menu bên trái), chọn **Users** -> Bấm **Create user** để tiến hành tạo IAM User:

![Create User](/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.1.png)

2. Thiết lập các thông tin cần thiết:

- **Bước 1**: Tiến hành đặt tên cho IAM User:

![Set User Name](/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.2.png)

- **Bước 2**: Thêm user vào nhóm `ExamoraAdminGroup` vừa tạo để gán quyền quản trị cho user:

![Add User to Group](/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.3.png)

- **Bước 3**: Kiểm tra lại thông tin và nhấn **Create user** để hoàn tất tạo IAM User:

![Review and Create](/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.4.png)

- Tương tự, tiến hành tạo thêm các IAM user cho các thành viên khác trong nhóm nhưng với phân quyền phù hợp và thấp hơn.
- Việc phân quyền này giúp quản lý quyền hạn rõ ràng hơn, giảm nguy cơ dùng chung tài khoản Root hoặc dùng chung một IAM user cho nhiều người.

![IAM Users List](/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.5.png)

3. Tiếp tục bật MFA cho IAM user nhằm tăng cường bảo mật khi đăng nhập AWS Console:

{{% notice note %}}
Về access key, nhóm chỉ tạo cho user cần sử dụng AWS CLI hoặc SAM để deploy hoặc dọn dẹp tài nguyên. Không tạo access key cho toàn bộ thành viên.
{{% /notice %}}

- Click vào user cần bật MFA, chọn tab **Security credentials**.
- Ở mục **Multi-factor authentication (MFA)**, chọn **Assign MFA device**:

![Assign MFA Device](/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.6.png)

- Đặt tên cho thiết bị MFA và lựa chọn phương thức xác thực tương ứng:

![Set MFA Device](/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.7.png)
