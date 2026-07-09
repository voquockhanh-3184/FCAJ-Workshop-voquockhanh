---
title : "Tạo HTTP API và gắn Lambda Backend"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.6.1. </b> "
---

#### Các bước thực hiện:

1. Tạo HTTP API:
   * Điều hướng đến dịch vụ **API Gateway** -> Chọn **HTTP API** để tiến hành tạo API mới.
   * Cấu hình API:
     * **API name**: Đặt tên cho API (ví dụ: `examora-api`).
     * **IP address type**: Chọn `IPv4`.
     * **Integration**: Chọn **Lambda**, sau đó điền **AWS Region** và **Lambda function** đã tạo ở phần trước (`examora-backend-api`).

   ![Cấu hình API](/images/5-Workshop/5.6-API-Gateway/5.6.1-create-http-api/API6.2.png)

2. Cấu hình Route cho backend Express:
   * Tạo các routes sau để ánh xạ request tới Lambda Backend:
     * **Route 1**: Method `GET`, Path `/health` (dùng để test public trước khi cấu hình xác thực).
     * **Route 2**: Method `ANY`, Path `/{proxy+}` (cho phép API Gateway forward tất cả các API endpoint hiện có của backend Examora như `/api/auth/me`, `/api/lop-hoc`, `/api/lich-su-thi`...).

   ![Cấu hình Route](/images/5-Workshop/5.6-API-Gateway/5.6.1-create-http-api/API6.3.png)

3. Cấu hình Stage và hoàn tất:
   * Bấm **Next** để sang bước 3 (Configure stages). Ở phần stage, giữ nguyên giá trị mặc định (`$default`) không thay đổi.
   * Bấm **Next** để kiểm tra lại cấu hình lần cuối (Review and create).

   ![Cấu hình Stage](/images/5-Workshop/5.6-API-Gateway/5.6.1-create-http-api/API6.4.png)

   * Nhấn **Create** và đợi thông báo tạo API thành công.

   ![Tạo thành công HTTP API](/images/5-Workshop/5.6-API-Gateway/5.6.1-create-http-api/API6.5.png)
