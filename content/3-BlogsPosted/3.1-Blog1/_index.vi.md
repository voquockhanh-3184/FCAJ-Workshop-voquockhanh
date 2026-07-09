---
title: "Blog 1"
date: 2026-07-05
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Tự động hóa Refresh Dữ liệu giữa các Tài khoản AWS cho Amazon RDS Multi-AZ DB Cluster

Việc tự động hóa refresh dữ liệu giữa các tài khoản AWS cho Amazon RDS Multi-AZ DB Cluster giúp đồng bộ dữ liệu production sang các môi trường staging hoặc testing mà không cần thao tác thủ công. Giải pháp sử dụng kiến trúc serverless kết hợp nhiều dịch vụ AWS để tự động hóa toàn bộ quy trình, đồng thời đảm bảo tính bảo mật khi dữ liệu được chia sẻ giữa các tài khoản.

Các điểm chính cần nắm:

* Amazon RDS không hỗ trợ chia sẻ trực tiếp cluster snapshot của Multi-AZ DB Cluster giữa các AWS accounts, nên cần sử dụng quy trình trung gian.
* Giải pháp thực hiện bằng cách:
Tạo cluster snapshot từ Multi-AZ DB Cluster.
Restore snapshot thành Single-AZ DB Instance tạm thời.
Tạo DB instance snapshot từ instance này.
Chia sẻ snapshot sang tài khoản đích và restore thành cơ sở dữ liệu mới.
* Toàn bộ quy trình được tự động hóa bằng kiến trúc serverless, không cần máy chủ quản lý.
* AWS Lambda thực hiện các tác vụ như tạo snapshot, restore database, chia sẻ snapshot và dọn dẹp tài nguyên tạm.
* AWS Step Functions điều phối toàn bộ workflow nhiều bước, theo dõi trạng thái của các tác vụ RDS và chỉ chuyển sang bước tiếp theo khi thao tác trước đã hoàn thành.
* Amazon EventBridge truyền sự kiện giữa tài khoản nguồn và tài khoản đích, giúp kích hoạt tự động các bước tiếp theo mà không cần can thiệp thủ công.
* Dữ liệu được bảo vệ bằng AWS KMS với customer-managed KMS key, đảm bảo snapshot luôn được mã hóa trong suốt quá trình chia sẻ giữa các tài khoản.
* Khi snapshot được copy sang tài khoản đích, dữ liệu sẽ được giải mã bằng KMS key của tài khoản nguồn và mã hóa lại bằng KMS key của tài khoản đích, đáp ứng yêu cầu bảo mật và phân tách quyền quản lý khóa.
* Giải pháp phù hợp cho các doanh nghiệp triển khai mô hình multi-account trên AWS, giúp đồng bộ dữ liệu nhanh chóng, tăng hiệu quả vận hành và đảm bảo tính bảo mật.


![Ảnh blog 1](/images/blog1.png)

[Link blog](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2200228570742103/#)

![Cấu trúc](/images/instructionblog1.png)