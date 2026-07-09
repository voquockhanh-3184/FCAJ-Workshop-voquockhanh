---
title : "Build và đóng gói Frontend"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.9.3. </b> "
---

#### Các bước thực hiện:

1. Biên dịch dự án Frontend (React/Vite):
   * Mở terminal tại thư mục code nguồn Frontend của bạn.
   * Chạy lệnh biên dịch mã nguồn thành phiên bản tối ưu hóa cho môi trường Production:
     ```bash
     npm run build
     ```
   * Sau khi biên dịch hoàn tất, hệ thống sẽ tự động khởi tạo thư mục `dist/` chứa toàn bộ tài nguyên tĩnh (HTML, CSS, JavaScript, Images,...).

   ![Biên dịch Frontend thành công](/images/5-Workshop/5.9-Amplify-Route53/5.9.3-build-frontend/BuildFE.png)

2. Đóng gói tệp tin:
   * Tiến hành nén toàn bộ nội dung trong thư mục `dist/`.
   * **Lưu ý quan trọng:** Bạn phải mở hẳn vào bên trong thư mục `dist/`, bôi đen toàn bộ các file/thư mục con và tiến hành nén thành file dạng `.zip` (ví dụ: `dist.zip`). Không nén trực tiếp cả thư mục cha `dist/` từ bên ngoài để tránh làm sai lệch cấu trúc đường dẫn root khi deploy lên AWS Amplify.

   ![Nén nội dung thư mục dist](/images/5-Workshop/5.9-Amplify-Route53/5.9.3-build-frontend/BuildFE2.png)
