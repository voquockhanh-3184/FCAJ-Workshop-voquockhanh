---
title : "Tạo nhóm quản trị IAM"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.2.3. </b> "
---

1. Trong **IAM Dashboard** (menu bên trái), tìm và chọn **User groups**, sau đó bấm vào **Create group**:

![Create Group](/images/5-Workshop/5.2-IAM/5.2.3-create-admin-group/IAM2.1.png)

2. Đặt tên cho nhóm IAM (ví dụ: `ExamoraAdminGroup`):

![Set Group Name](/images/5-Workshop/5.2-IAM/5.2.3-create-admin-group/IAM2.2.png)

3. Gán policy quản trị: Kéo xuống phần **Attach permissions policies - Optional**, tìm và tích chọn **AdministratorAccess** -> Bấm **Create user group** để tiến hành tạo.

![Attach AdministratorAccess](/images/5-Workshop/5.2-IAM/5.2.3-create-admin-group/IAM2.3.png)

{{% notice info %}}
**AdministratorAccess** được sử dụng tạm thời cho giai đoạn cấu hình ban đầu.
{{% /notice %}}

4. Tạo nhóm người dùng thành công:

![Group Created Successfully](/images/5-Workshop/5.2-IAM/5.2.3-create-admin-group/IAM2.4.png)
