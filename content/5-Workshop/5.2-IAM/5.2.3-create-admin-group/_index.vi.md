---
title : "Tạo nhóm quản trị viên IAM Admin Group"
date : 2026-07-09 
weight : 3
chapter : false
pre : " <b> 5.2.3. </b> "
---

1. Tại giao diện **IAM Dashboard** (menu bên trái), tìm và chọn mục **User groups**, sau đó nhấn chọn **Create group**:

![Tạo Nhóm](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.2-IAM/5.2.3-create-admin-group/IAM2.1.png)

2. Nhập tên cho nhóm IAM (Ví dụ: `ExamoraAdminGroup`):

![Đặt Tên Nhóm](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.2-IAM/5.2.3-create-admin-group/IAM2.2.png)

3. Đính kèm chính sách quản trị viên: Cuộn xuống phần **Attach permissions policies - Optional**, tìm kiếm và tích chọn **AdministratorAccess** -> Nhấn **Create user group** để hoàn tất tạo nhóm.

![Đính kèm quyền AdministratorAccess](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.2-IAM/5.2.3-create-admin-group/IAM2.3.png)

{{% notice info %}}
Quyền **AdministratorAccess** được sử dụng tạm thời cho giai đoạn cấu hình ban đầu.
{{% /notice %}}

4. Nhóm người dùng đã được tạo thành công:

![Tạo Nhóm Thành Công](/FCAJ-Workshop-voquockhanh/images/5-Workshop/5.2-IAM/5.2.3-create-admin-group/IAM2.4.png)