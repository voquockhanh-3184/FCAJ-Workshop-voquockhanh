---
title : "Tạo Lambda Function"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.5.3. </b> "
---

Trong bước này, chúng ta sẽ tạo Lambda function chính đóng vai trò xử lý toàn bộ backend Express của hệ thống Examora.

#### Các bước thực hiện:

1. Tạo Lambda Function:
   * Trên thanh tìm kiếm của AWS Console, nhập **Lambda** -> Chọn **Functions** ở menu trái -> Bấm **Create function**.
   * Chọn **Author from scratch** (Tạo mới từ đầu).
   * Cấu hình các thông tin cơ bản:
     * **Function name**: Nhập `examora-backend-api`.
     * **Runtime**: Chọn **Node.js 22.x** 
     * **Architecture**: Chọn **x86_64**.
     * **Permissions**: Mở rộng phần **Change default execution role** -> Chọn **Use an existing role** -> Tìm và chọn IAM execution role đã tạo ở bước trước (`examora-lambda-backend-role`).
   * Bấm nút **Create function** ở góc dưới cùng và đợi hệ thống khởi tạo.

   ![Cấu hình tạo Function](/images/5-Workshop/5.5-Lambda/5.5.3-create-lambda-function/LamdaFuctions5.1.png)

   ![Chọn Execution Role](/images/5-Workshop/5.5-Lambda/5.5.3-create-lambda-function/LamdaFuctions5.2.png)

2. Cấu hình Lambda Runtime Settings:
   * Vào function vừa tạo -> **Configuration** -> **General configuration** -> chọn **Edit**, cấu hình cho Express backend phù hợp -> Nhấn **Save**.

   ![Cấu hình General Configuration](/images/5-Workshop/5.5-Lambda/5.5.3-create-lambda-function/LamdaFuctions5.3.png)
