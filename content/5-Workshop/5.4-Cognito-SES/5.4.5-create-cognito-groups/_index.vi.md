---
title : "Tạo Cognito Groups cho Examora"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.4.5. </b> "
---

#### Mục tiêu:
Khởi tạo các **Cognito User Groups** nhằm phân loại vai trò nghiệp vụ (Role-based access control) của người dùng trong hệ thống Examora.

Hệ thống quản lý thi Examora có 3 nhóm người dùng chính:

| Cognito Group | Vai trò | Mô tả quyền hạn |
|---|---|---|
| **ADMIN** | Quản trị hệ thống | Quản trị toàn bộ hạ tầng, thiết lập cấu hình hệ thống. |
| **TEACHER** | Giảng viên | Quản lý lớp học, soạn đề thi, quản lý ngân hàng câu hỏi. |
| **STUDENT** | Học viên / Sinh viên | Tham gia các bài thi trắc nghiệm trực tuyến, xem kết quả làm bài. |

**Cơ chế hoạt động:**
*   **Cognito Groups** cho phép nhóm người dùng theo vai trò nghiệp vụ. Sau khi người dùng đăng nhập thành công, Cognito sẽ đính kèm thông tin nhóm này vào JWT (ID Token) thông qua claim `cognito:groups`.
*   Phía Backend (Lambda API) sẽ giải mã JWT và đọc claim `cognito:groups` này để quyết định từ chối hoặc cho phép truy cập tài nguyên (authorization).

#### Các bước thực hiện:

1. Trong giao diện chi tiết của User Pool vừa tạo, chuyển sang tab **Groups** -> Chọn **Create group**.
2. Tiến hành tạo lần lượt 3 group với tên chính xác: `ADMIN`, `TEACHER`, `STUDENT` -> Nhấn chọn **Create group** cho mỗi nhóm để hoàn tất.

![Create Group](/images/5-Workshop/5.4-Cognito-SES/COGNITO4.6.png)
