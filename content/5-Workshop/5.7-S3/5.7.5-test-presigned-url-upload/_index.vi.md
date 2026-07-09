---
title : "Kiểm thử Presigned URL Endpoint và Upload file lên S3"
date : 2024-01-01 
weight : 5
chapter : false
pre : " <b> 5.7.5. </b> "
---

#### Mục tiêu:
Kiểm tra endpoint tạo presigned URL đã được bảo vệ chính xác bởi API Gateway kết hợp Cognito JWT Authorizer, đồng thời xác nhận xem tệp tin tải lên (upload) bằng presigned URL đã hiển thị thành công trong S3 Upload Bucket hay chưa.

---

#### Test 1: Gọi endpoint presigned URL không có JWT
*   **Kết quả mong đợi**: Trả về lỗi `401 Unauthorized` từ API Gateway.
*   **Kết quả thực tế**:

   ![Test 1: Yêu cầu không có JWT](/images/5-Workshop/5.7-S3/5.7.5-test-presigned-url-upload/TestURL1.png)

---

#### Test 2: Gọi endpoint presigned URL có JWT
*   **Bước 1**: Đăng nhập tài khoản giảng viên trên Frontend Examora để lấy chuỗi Cognito JWT.
*   **Bước 2**: Mở Console trong DevTools của trình duyệt và gửi request có header Authorization chứa token.
*   **Kết quả mong đợi**: HTTP Status trả về `200` và trả về JSON có cấu trúc:
   ```json
   {
     "uploadUrl": "https://...",
     "bucket": "...",
     "objectKey": "imports/word/raw/<teacherId>/<uuid>.docx",
     "method": "PUT",
     "expiresIn": 300
   }
   ```
*   **Kết quả thực tế**:

   ![Test 2: Request có JWT hợp lệ](/images/5-Workshop/5.7-S3/5.7.5-test-presigned-url-upload/TestURL2.png)

---

#### Test 3: Upload tệp tin lên S3 bằng Presigned URL
*   Ngay sau khi lấy được `uploadUrl` từ Test 2, chạy đoạn script sau trong Console để thực hiện upload file `.docx` trực tiếp lên S3 Upload Bucket:

```javascript
const input = document.createElement("input");
input.type = "file";
input.accept = ".docx";

input.onchange = async () => {
  const file = input.files[0];

  const res = await fetch(window.examoraUploadUrl, {
    method: "PUT",
    headers: {
      "Content-Type": "application/vnd.openxmlformats-officedocument.wordprocessingml.document"
    },
    body: file
  });

  console.log("S3 upload status:", res.status);
  console.log("S3 key:", window.examoraUploadKey);
};

input.click();
```

*   **Bước 1**: Chọn một tệp tin `.docx` bất kỳ trên máy tính để tải lên.
*   **Kết quả thu được**: In ra log console `S3 upload status: 200` (thành công).

   ![Test 3: Log upload thành công](/images/5-Workshop/5.7-S3/5.7.5-test-presigned-url-upload/TestURL3.png)

*   **Bước 2**: Kiểm tra trực tiếp trên Amazon S3 Console:
    *   Điều hướng đến trang **Buckets** -> Chọn vào tên bucket đã tạo -> Chọn mục **Objects** -> Tìm đến đường dẫn thư mục `imports/word/raw/<teacherId>/`.
    *   Nếu thấy xuất hiện file `.docx` vừa upload thì luồng tải lên trực tiếp đã hoạt động chính xác.

   ![Kiểm tra tệp tin trên S3](/images/5-Workshop/5.7-S3/5.7.5-test-presigned-url-upload/TestURL4.png)
