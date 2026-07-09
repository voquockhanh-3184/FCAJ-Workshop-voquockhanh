---
title : "Quy ước tiền tố đường dẫn (Prefix) tổ chức file"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.7.2. </b> "
---

Examora sử dụng một S3 Upload Bucket chung duy nhất và phân loại tổ chức lưu trữ các tệp tin theo các tiền tố đường dẫn (prefix) khác nhau tùy thuộc vào nghiệp vụ hệ thống:

| Loại file | Upload type | Prefix đề xuất | Quyền upload |
| :--- | :--- | :--- | :--- |
| **Avatar người dùng** | `avatar` | `avatars/{userId}/` | ADMIN, TEACHER, STUDENT |
| **Ảnh bìa lớp học** | `classCover` | `classes/{classId}/cover/` | ADMIN, TEACHER |
| **Ảnh minh họa đề thi** | `examImage` | `exams/{examId}/images/` | ADMIN, TEACHER |
| **File Word import thô** | `wordImport` | `imports/word/raw/{teacherId}/` | ADMIN, TEACHER |

#### Tác dụng:
*   **Tổ chức tài nguyên khoa học:** Giúp phân cấp thư mục tệp tin rõ ràng trên S3 bucket.
*   **Kiểm soát an ninh chặt chẽ:** Lambda Backend có thể xác thực JWT của request và kiểm tra phân quyền (Role/Groups) của user trước khi ký cấp phát Presigned URL, đảm bảo user không thể upload file trái phép hoặc ghi đè lên tài nguyên của user khác.
