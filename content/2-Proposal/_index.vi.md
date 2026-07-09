---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Examora - Online Exam Platform
## Giải pháp AWS Serverless cho nền tảng thi trực tuyến

### 1. Tóm tắt điều hành
Examora là nền tảng thi trắc nghiệm trực tuyến dành cho ba nhóm người dùng: quản trị viên, giáo viên và học sinh. Hệ thống hỗ trợ đăng ký/đăng nhập, quản lý lớp học, quản lý đề thi, import câu hỏi từ file Word, làm bài trực tuyến, chấm điểm tự động và xem lịch sử kết quả.

Dự án được đề xuất chuyển đổi sang kiến trúc AWS Serverless. Frontend React/Vite được triển khai bằng AWS Amplify Hosting và gắn domain thông qua Route 53. Xác thực người dùng sử dụng Amazon Cognito kết hợp Amazon SES để gửi OTP email và reset password. Backend Express hiện có được đóng gói chạy trên AWS Lambda, nhận request thông qua API Gateway HTTP API với Cognito JWT Authorizer. MongoDB Atlas tiếp tục là database chính nhằm tránh thay đổi lớn về schema và dữ liệu hiện có.

Các chức năng xử lý file và tác vụ nặng được tách ra theo hướng bất đồng bộ. File upload như avatar, ảnh lớp học, ảnh đề thi, ảnh câu hỏi và file Word được lưu trong S3 Upload Bucket thông qua presigned URL. File Word sau khi upload sẽ kích hoạt Lambda Import Word Processor để parse và lưu câu hỏi vào MongoDB. Luồng nộp bài được tách khỏi luồng chấm bài bằng Amazon SQS và Lambda Grading Worker để tránh request bị chậm hoặc timeout.

Mục tiêu của proposal là xây dựng một nền tảng web thi trực tuyến có xác thực an toàn, triển khai gọn, dễ mở rộng, giảm vận hành server thủ công và vẫn tận dụng được logic nghiệp vụ hiện có của dự án Examora.

### 2. Tuyên bố vấn đề
*Vấn đề hiện tại*

Phiên bản ban đầu của Examora hoạt động theo mô hình web truyền thống với frontend React, backend Express và MongoDB. Cách triển khai này đáp ứng được nghiệp vụ cơ bản, nhưng khi chuyển sang môi trường triển khai thực tế sẽ gặp một số vấn đề:

- Xác thực tự quản bằng JWT/local token khó mở rộng và khó tích hợp các luồng OTP email, reset password, phân quyền tập trung.
- Upload file dựa vào backend/local storage không phù hợp khi chạy trên môi trường serverless, vì Lambda không nên lưu file lâu dài trong filesystem.
- Chấm bài trực tiếp trong request nộp bài dễ làm request chậm, khó retry nếu xử lý lỗi.
- Import câu hỏi từ Word là tác vụ xử lý file, cần tách khỏi request chính để tránh ảnh hưởng trải nghiệm người dùng.
- Backend cần cơ chế quản lý secret, log, tracing và quyền truy cập dịch vụ rõ ràng hơn.
- Frontend cần một phương án deploy đơn giản, hỗ trợ domain riêng và phù hợp với React SPA.

*Giải pháp*

Examora sử dụng AWS Serverless để tách hệ thống thành các khối rõ ràng:

- Route 53 quản lý domain `examora.click`.
- AWS Amplify Hosting triển khai frontend React/Vite và xử lý rewrite cho React Router.
- Amazon Cognito quản lý user pool, email/password và Cognito Groups gồm `ADMIN`, `TEACHER`, `STUDENT`.
- Amazon SES gửi OTP đăng ký và email reset password thông qua Cognito.
- API Gateway HTTP API kiểm tra Cognito JWT trước khi route request vào Lambda Backend API.
- Lambda Backend API chạy Express backend hiện tại bằng `serverless-http`.
- MongoDB Atlas tiếp tục lưu dữ liệu chính: người dùng, lớp học, bài giảng, câu hỏi, kết quả bài thi.
- S3 Upload Bucket lưu file nghiệp vụ bằng presigned URL.
- Lambda Import Word Processor xử lý file Word sau khi upload lên S3.
- Amazon SQS và Lambda Grading Worker xử lý chấm bài bất đồng bộ.
- Secrets Manager lưu MongoDB URI và cấu hình nhạy cảm.
- CloudWatch Logs và X-Ray hỗ trợ giám sát, debug và trace request.

### 3. Kiến trúc giải pháp
Kiến trúc Examora được chia thành các nhóm chính: frontend hosting, authentication, core API, upload/import pipeline, grading pipeline, monitoring và security configuration.

![Examora Architecture](/images/2-Proposal/Examora_Architecture_Final2.png)

*Dịch vụ AWS sử dụng*

- *Route 53*: Quản lý domain `examora.click` và trỏ về Amplify Hosting.
- *AWS Amplify Hosting*: Triển khai frontend React/Vite, phục vụ SPA và hỗ trợ custom domain.
- *Amazon Cognito*: Quản lý đăng ký, đăng nhập, JWT và Cognito Groups.
- *Amazon SES*: Gửi email OTP và reset password.
- *Amazon API Gateway*: Public API endpoint, xác thực JWT bằng Cognito Authorizer.
- *AWS Lambda*: Chạy Backend API, Import Word Processor và Grading Worker.
- *Amazon S3 Upload Bucket*: Lưu avatar, ảnh lớp học, ảnh đề thi, ảnh câu hỏi và file Word import.
- *Amazon SQS*: Hàng đợi chấm bài, tách request nộp bài khỏi xử lý chấm điểm.
- *AWS Secrets Manager*: Lưu MongoDB URI và secret config.
- *Amazon CloudWatch*: Ghi log Lambda và theo dõi lỗi runtime.
- *AWS X-Ray*: Trace request và phân tích độ trễ.
- *AWS IAM*: Cấp quyền tối thiểu cho từng Lambda và dịch vụ liên quan.
- *MongoDB Atlas*: Database chính bên ngoài AWS, lưu toàn bộ dữ liệu nghiệp vụ.

*Thiết kế thành phần*

- *Frontend*: React/Vite SPA được build và deploy lên Amplify Hosting. Frontend gọi Cognito để đăng nhập, sau đó gửi JWT trong header `Authorization` khi gọi API Gateway.
- *Authentication*: Sử dụng Amazon Cognito để quản lý tài khoản người dùng, hỗ trợ xác thực qua mã OTP và phân quyền theo các nhóm vai trò nghiệp vụ (như quản trị viên, giáo viên, học sinh) đồng bộ sang cơ sở dữ liệu chính.
- *Core API*: API Gateway nhận request từ frontend, validate JWT, sau đó chuyển request hợp lệ vào Lambda Backend API.
- *Backend API*: Express backend xử lý nghiệp vụ lớp học, bài giảng, câu hỏi, profile, upload, lịch sử thi và nộp bài.
- *Upload pipeline*: Backend tạo presigned URL, frontend upload file trực tiếp lên S3 Upload Bucket, backend lưu object key vào MongoDB.
- *Word import pipeline*: S3 ObjectCreated event kích hoạt Lambda Import Word Processor để parse file `.docx` và lưu câu hỏi vào MongoDB.
- *Grading pipeline*: Backend lưu bài nộp ở trạng thái đang chấm, gửi job vào SQS, Lambda Grading Worker chấm điểm và cập nhật kết quả.
- *Monitoring và security*: Lambda ghi log vào CloudWatch, trace qua X-Ray, đọc secret từ Secrets Manager và hoạt động theo IAM Role riêng.

### 4. Triển khai kỹ thuật
*Các giai đoạn triển khai kỹ thuật*

1. *Chuẩn hóa xác thực*: Cấu hình Cognito User Pool, SES, Cognito Groups và cập nhật frontend/backend để dùng Cognito JWT.
2. *Đưa backend lên Lambda*: Tách Express app khỏi `server.listen()`, thêm Lambda handler, đóng gói backend và deploy Lambda Backend API.
3. *Cấu hình API Gateway*: Tạo HTTP API tích hợp với mã xử lý Backend, thiết lập cơ chế kiểm tra token bảo mật cho các đường dẫn truyền nhận dữ liệu, cấu hình CORS và tiến hành kiểm tra kết nối hệ thống cơ bản.
4. *Cấu hình upload file*: Tạo S3 Upload Bucket, cấp IAM cho Lambda Backend API, xây endpoint presigned URL và chuyển flow upload avatar/ảnh/file Word sang S3.
5. *Tách tác vụ Import Word*: Xây dựng hàm Lambda chuyên biệt xử lý file Word tải lên S3 thông qua cơ chế kích hoạt sự kiện tự động khi tải tài liệu thành công, tiến hành trích xuất câu hỏi và lưu trữ dữ liệu.
6. *Tách chấm bài*: Tạo SQS Grading Queue, Lambda Grading Worker, cập nhật backend để lưu bài nộp rồi gửi grading job vào SQS.
7. *Triển khai frontend*: Build frontend React/Vite, deploy lên Amplify Hosting, cấu hình rewrite cho React Router và kết nối với API Gateway.
8. *Gắn domain và giám sát*: Cấu hình Route 53 cho domain `examora.click`, kiểm tra CloudWatch Logs, X-Ray và các biến môi trường production.

*Yêu cầu kỹ thuật*

- Frontend React/Vite phải đọc `VITE_BACKEND_URL` trỏ đến API Gateway endpoint.
- Backend Lambda cần các cấu hình biến môi trường phục vụ việc kết nối cơ sở dữ liệu, tham chiếu dịch vụ lưu trữ dữ liệu, cấu hình hàng đợi thông điệp và danh sách các tên miền Frontend được phép gọi API.
- MongoDB URI được lưu trong Secrets Manager, không hard-code trong source code hoặc Lambda environment variables.
- S3 Upload Bucket giữ private, truy cập thông qua presigned PUT/GET URL.
- API Gateway dùng Cognito JWT Authorizer để chặn request không có token hợp lệ.
- Hàm Lambda xử lý Backend thực hiện kiểm tra độ hợp lệ của mã token JWT nhận từ người dùng và tiến hành đồng bộ thông tin hồ sơ tài khoản vào cơ sở dữ liệu.
- IAM Role cần được tách theo chức năng: Backend API, Import Word Processor và Grading Worker.
- CORS cần cho phép local dev, Amplify domain và domain chính thức.

### 5. Lộ trình & Mốc triển khai
*   **Trước thực tập:** Lên kế hoạch sơ khởi và phân tích hiện trạng dự án Examora.
*   **Thực tập (Tháng 4 - Tháng 7):**
    *   **Tháng 4:** Tìm hiểu lý thuyết và thực hành theo các tài liệu hướng dẫn về dịch vụ đám mây của AWS.
    *   **Tháng 5:** Lên kế hoạch chi tiết, phân tích yêu cầu, thiết kế kiến trúc hệ thống (AWS Architecture) cho dự án Examora.
    *   **Tháng 6 - 7:** Tiến hành triển khai hạ tầng Serverless, kiểm thử hệ thống tích hợp (E2E), tối ưu hóa tài nguyên và hoàn thiện báo cáo dự án.
*   **Sau triển khai:** Tiếp tục theo dõi, vận hành và tối ưu hóa hệ thống serverless.

### 6. Ước tính ngân sách
Có thể xem chi phí trên AWS Pricing Calculator theo file estimate đã xuất.
Hoặc tải [tệp ước tính ngân sách](/images/2-Proposal/ExamoraCost.pdf).

*Chi phí hạ tầng*

- AWS Amplify: 0,62 USD/tháng (Standard build instance, 1 GB lưu trữ, 60 build minutes/tháng, 0 SSR request).
- Amazon Cognito: 0,01 USD/tháng (1.000 monthly active users, advanced security disabled).
- Amazon API Gateway: 0,01 USD/tháng (HTTP API, 10.000 request/tháng, trung bình 2 KB/request).
- AWS Lambda: 0,00 USD/tháng (10.000 request/tháng, 512 MB ephemeral storage).
- Amazon S3 Standard: 0,16 USD/tháng (5 GB/tháng, 5.000 PUT/COPY/POST/LIST request, 50.000 GET request).
- Amazon SQS: 0,00 USD/tháng (Standard Queue request ở mức thấp).
- Amazon SES: 0,15 USD/tháng (1.000 email/tháng).
- AWS Secrets Manager: 0,50 USD/tháng (1 secret, 20.000 API call/tháng).
- Amazon Route 53: 0,50 USD/tháng (1 hosted zone).
- AWS X-Ray: 0,01 USD/tháng (1.000 request/tháng, sampling rate 1).
- Amazon CloudWatch: 0,50 USD/tháng (1 GB log ingested và metric/log cơ bản).

*Tổng*: 2,46 USD/tháng, 29,52 USD/12 tháng.

Ghi chú: Con số trên là ước tính từ AWS Pricing Calculator và có thể thay đổi theo region, lưu lượng request, dung lượng file upload, số lượng user thực tế và mức log phát sinh.

### 7. Đánh giá rủi ro
*Ma trận rủi ro*

- Cấu hình JWT/Cognito sai: Ảnh hưởng cao, xác suất trung bình.
- CORS sai giữa Amplify domain, local dev và API Gateway: Ảnh hưởng trung bình, xác suất cao trong giai đoạn triển khai.
- Lambda timeout khi xử lý import Word hoặc chấm bài: Ảnh hưởng trung bình, xác suất trung bình.
- SQS message không được worker xử lý đúng: Ảnh hưởng cao, xác suất thấp đến trung bình.
- MongoDB Atlas network access hoặc secret sai: Ảnh hưởng cao, xác suất trung bình.
- Quyền IAM quá rộng hoặc thiếu quyền cần thiết: Ảnh hưởng cao, xác suất trung bình.
- Chi phí log/file upload tăng ngoài dự kiến: Ảnh hưởng trung bình, xác suất thấp.

*Chiến lược giảm thiểu*

- Kiểm tra JWT bằng cả API Gateway Authorizer và backend middleware.
- Dùng `FRONTEND_ORIGINS` để quản lý nhiều origin hợp lệ cho local, Amplify và domain chính thức.
- Tách import Word và chấm bài sang Lambda riêng để tránh làm chậm request chính.
- Ghi vết chi tiết thông tin định danh của các bài thi và học sinh tương ứng khi gửi tác vụ chấm điểm nhằm hỗ trợ theo dõi luồng thông điệp qua hàng đợi.
- Lưu MongoDB URI trong Secrets Manager và kiểm tra quyền `secretsmanager:GetSecretValue` cho từng Lambda.
- Giới hạn IAM theo đúng bucket, queue và secret cần dùng.
- Cấu hình CloudWatch log retention và AWS Budget Alert nếu đưa vào môi trường chạy dài ngày.

*Kế hoạch dự phòng*

- Nếu Lambda Grading Worker lỗi, dữ liệu bài nộp vẫn nằm trong MongoDB với trạng thái đang chấm và có thể retry job.
- Nếu Import Word Processor lỗi, file gốc vẫn nằm trong S3 Upload Bucket để xử lý lại.
- Nếu Amplify deployment lỗi, có thể rollback về bản build trước trong Amplify Console.
- Nếu Cognito group chưa đúng, admin có thể cập nhật group trên Cognito Console và user đăng nhập lại để nhận JWT mới.

### 8. Kết quả kỳ vọng
*Cải tiến kỹ thuật*

Examora chuyển từ mô hình web backend truyền thống sang kiến trúc AWS Serverless có xác thực tập trung, backend chạy Lambda, upload file qua S3, import Word bất đồng bộ và chấm bài qua SQS Worker. Hệ thống giảm phụ thuộc vào server tự quản và dễ kiểm tra lỗi thông qua CloudWatch/X-Ray.

*Giá trị dài hạn*

- **Nâng cao hiệu suất giảng dạy và tối ưu công sức:** Giúp giáo viên giảm thiểu tối đa thời gian soạn đề nhờ tính năng nhập câu hỏi tự động từ tài liệu sẵn có, đồng thời loại bỏ hoàn toàn công việc chấm bài thủ công nhờ hệ thống chấm điểm tự động và chính xác.
- **Nâng cao trải nghiệm học tập của học sinh:** Cung cấp cho học sinh một nền tảng thi trực tuyến tiện lợi, thân thiện, cho phép làm bài trực tuyến mọi lúc mọi nơi và theo dõi lịch sử kết quả thi tức thời để tự đánh giá và nâng cao kết quả học tập.
- **Tiết kiệm chi phí đầu tư và vận hành:** Giúp các tổ chức giáo dục tối ưu hóa chi phí hạ tầng công nghệ thông tin nhờ mô hình thanh toán theo lưu lượng sử dụng thực tế của điện toán đám mây, giảm thiểu gánh nặng nhân sự vận hành máy chủ vật lý truyền thống mà vẫn đảm bảo tính ổn định trong các kỳ thi tập trung đông người.

