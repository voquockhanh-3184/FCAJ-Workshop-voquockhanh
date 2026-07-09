---
title: "Event 1"
date: 2026-05-23
weight: 1
chapter: false
---

# Báo Cáo Workshop: AI & Cloud Modernization

## 1. Mục đích của sự kiện

Buổi workshop mang đến cho người tham gia những góc nhìn thực tế về các xu hướng công nghệ **AI và Điện toán đám mây (Cloud)** hiện nay, giúp người học:

- Nhận thức rõ vai trò cốt lõi của **Ngữ cảnh (Context)** trong việc tối ưu hóa hiệu năng và khai thác AI.
- Khám phá hệ sinh thái AI trên nền tảng đám mây do Amazon phát triển dành riêng cho các bài toán doanh nghiệp.
- Nâng cao kiến thức kỹ thuật về **Amazon CloudFront** trong việc tối ưu hiệu năng, thắt chặt bảo mật và giảm thiểu chi phí.
- Tích lũy kinh nghiệm phát triển sản phẩm thực chiến dưới áp lực thời gian lớn từ môi trường thi đấu Hackathon.
- Thấu hiểu sâu sắc các giới hạn tính toán cơ bản của các mô hình ngôn ngữ lớn (LLM), đặc biệt là tính không xác định (**Non-determinism**).
- Tiếp cận các mô hình thiết kế hệ thống **Multi-Agent System** trong quy trình tự động hóa nghiệp vụ doanh nghiệp.

---

## 2. Danh sách diễn giả

- Tinh Truong
- Anh Pham
- Thinh Nguyen
- Team VIB
- Duc Dao
- Vy Lam

---

## 3. Nội dung nổi bật

### Context Is Everything: Making AI Actually Work for You

Phiên chia sẻ tập trung vào các chiến lược chuẩn hóa và tối ưu ngữ cảnh đầu vào để đảm bảo độ chính xác cao nhất cho dữ liệu do AI tạo ra.

**Các nội dung chính:**
- **Ngữ cảnh (Context)** là yếu tố quyết định hàng đầu đến độ chính xác về mặt ngữ nghĩa và chất lượng đầu ra của AI.
- Việc xây dựng một cấu trúc prompt tốt là chưa đủ; các mô hình LLM luôn đòi hỏi một nền tảng dữ liệu nền và ngữ cảnh đi kèm phải thật đầy đủ, tường minh.
- Giới thiệu mô hình cấu trúc hệ thống **Second AI Brain** (Bộ não AI thứ hai) nhằm thu thập, lưu trữ và truy xuất các thông tin vận hành một cách tự động, thông suốt.
- Chia sẻ các phương pháp thiết lập hệ thống AI cá nhân hóa nhằm tối ưu hóa hiệu quả nghiên cứu học thuật và định hình lộ trình phát triển sự nghiệp.

---

### Friendly AI Assistant with Amazon Quick

Phần giới thiệu về mặt kiến trúc và các tính năng hướng đến tối ưu hiệu suất làm việc của bộ công cụ **Amazon Quick**:

**Các thành phần cốt lõi:**
- **Quick Chat Agent:** Công cụ hỗ trợ giao tiếp cho phép chạy các truy vấn phân tích cơ sở dữ liệu phức tạp và phản hồi người dùng hoàn toàn bằng ngôn ngữ tự nhiên.
- **Quick Flows:** Giao diện trực quan giúp các đội ngũ kỹ sư thiết kế và điều phối các quy trình tự động hóa backend thông minh mà không cần trực tiếp viết mã nguồn.
- **Quick Spaces:** Không gian cộng tác an toàn, tập trung, hỗ trợ chia sẻ tài liệu nội bộ và đồng bộ hóa dữ liệu mượt mà giữa các thành viên trong nhóm.

---

### 36 Hours with LotusHacks – Building UTMorpho

Đội ngũ Team VIB chia sẻ chi tiết về vòng đời phát triển và triển khai sản phẩm thần tốc dưới áp lực thời gian nghiêm ngặt của cuộc thi:

**Các bài học kinh nghiệm:**
- Động lực cốt lõi khi quyết định dấn thân vào thử thách công nghệ đầy tính cạnh tranh tại LotusHacks.
- Quy trình phối hợp tư duy, phản biện và brainstorm ý tưởng kỹ thuật diễn ra trong những giờ đầu tiên của cuộc thi.
- Hành trình xây dựng thành công một sản phẩm khả dụng tối thiểu (MVP) hoàn chỉnh chỉ trong vòng 36 giờ đồng hồ nỗ lực liên tục.
- Cách nhận diện và vượt qua các lỗi tích hợp nghiêm trọng, quản trị rủi ro, kiểm soát áp lực và phân rã công việc hợp lý khi làm việc nhóm.
- Phiên trình diễn trực tiếp (Demo) cấu trúc kiến trúc phần mềm hoàn thiện của sản phẩm.
- Phân tích hậu cuộc thi về các bài học kỹ thuật thu được và cách xử lý nợ công nghệ (technical debt).

---

### From Edge To Origin: CloudFront as Your Foundation

Đi sâu vào các phương thức cấu hình tham số bộ nhớ đệm (caching) trên phạm vi toàn cầu nhằm bảo mật và tăng tốc hệ thống hạ tầng Cloud:

**Các nguyên lý cốt lõi:**
- Khả năng xử lý linh hoạt và chịu tải các loại hình dữ liệu web hỗn hợp (heterogeneous workloads) ở quy mô lớn của Amazon CloudFront.
- Loại bỏ chi phí băng thông truyền tải dữ liệu đầu ra (egress cost) và tối ưu ngân sách vận hành nhờ cơ chế phân phối dữ liệu CDN thông minh.
- Tăng cường các lớp bảo mật vòng ngoài tại biên mạng thông qua các cơ chế phòng vệ tích hợp của AWS.
- Tối đa hóa tính sẵn sàng của hệ thống (high availability) và thiết lập các giao thức dự phòng theo từng vùng địa lý.
- Giảm thiểu tối đa độ trễ phản hồi mạng nhờ vào mạng lưới các trung tâm điều phối dữ liệu biên (**Edge Locations**) toàn cầu của AWS.

---

## 4. Những kiến thức học được

### Kiến thức về Kỹ nghệ AI

Sau khi hoàn thành các nội dung chia sẻ, em đã nâng cao nhận thức về:

- Sự phụ thuộc tuyệt đối của mô hình vào các khối dữ liệu đầu vào có tính mô tả cao nhằm hạn chế tối đa hiện tượng "ảo tưởng" (hallucination) và định hướng độ chính xác.
- Các phương pháp nâng cao trong việc tổ chức và xây dựng prompt để bóc tách chính xác các khối mã nguồn logic hoặc chương trình phức tạp.
- Các ranh giới thuật toán của mạng neural, đặc biệt là cách kiểm soát biến số và tính không xác định (**Non-determinism**) trong thời gian thực.
- Xu hướng dịch chuyển công nghệ từ các công cụ AI cô lập sang các hệ thống trợ lý hoạt động cộng tác (**AI Agents** và **Multi-Agent Systems**).

---

### Kiến thức về Kiến trúc Hạ tầng Cloud

Các kiến thức kỹ thuật thu được bao gồm:

- Cơ chế vận hành thực tế của **Amazon CloudFront** trong việc tăng tốc độ lưu trữ đệm (caching) và tối ưu đường truyền tài nguyên trên toàn thế giới.
- Cách thức cấu hình bắt tay an toàn SSL/TLS, thiết lập ranh giới kiểm soát truy cập và nâng cao mục tiêu sẵn sàng của máy chủ gốc thông qua tầng tiền tuyến CDN.
- Tầm quan trọng của việc sử dụng tầng phân phối nội dung như một vùng đệm an toàn để giảm tải áp lực tính toán trực tiếp lên tài nguyên Cloud cốt lõi.

---

## 5. Ứng dụng vào học tập và công việc

Em sẽ áp dụng những bài học công nghệ này vào quá trình học tập cũng như các tác vụ phát triển phần mềm fullstack thực tế:

- Thiết kế các chuỗi chỉ dẫn giàu ngữ cảnh khi làm việc với các hệ thống AI hỗ trợ lập trình nhằm tối ưu hóa tính logic của mã nguồn generated.
- Thử nghiệm nền tảng **Amazon Quick** để tự động hóa việc phân tích dữ liệu cấu trúc và thiết kế nhanh các không gian dashboard phục vụ kiểm thử database.
- Tích hợp cấu hình CDN **Amazon CloudFront** khi triển khai các ứng dụng Single-Page (SPA) hoặc hệ thống backend để thiết lập quy tắc cache chuẩn xác và bảo vệ máy chủ gốc.
- Tinh chỉnh kỹ năng quản trị dự án linh hoạt (Agile) để cô đọng tính năng hiệu quả khi làm việc nhóm trong các dự án có timeline ngắn và nghiêm ngặt.
- Nghiên cứu sâu hơn về các kiến trúc phần mềm đa đại lý (multi-agent) để ứng dụng vào việc xây dựng các tác vụ chạy ngầm bất đồng bộ và tự động hóa hệ thống.

---

## 6. Trải nghiệm và Ấn tượng tại sự kiện

Việc tham gia buổi workshop mang lại những giá trị thực tiễn to lớn, giúp em kết nối thành công giữa các **mô hình lý thuyết AI** và tầng **hạ tầng mạng Cloud** cốt lõi.

Phiên thảo luận về **Ngữ cảnh trong các mô hình ngôn ngữ lớn** để lại ấn tượng mạnh mẽ. Nội dung này khẳng định rằng năng lực hỗ trợ của AI phụ thuộc rất lớn vào độ hoàn thiện và tính cấu trúc của khối dữ liệu được đưa vào bộ đệm đầu vào.

Thêm vào đó, khả năng tích hợp linh hoạt trong **Amazon Quick** minh chứng rõ ràng rằng các công cụ tự động hóa đang tiến hóa vượt bậc, không còn dừng lại ở các giao diện chat thông thường mà đã trở thành các engine điều phối mạnh mẽ cho các bài toán xử lý dữ liệu low-code trong doanh nghiệp.

Bài phân tích về hiệu năng của **Amazon CloudFront** cũng giúp em củng cố tư duy tối ưu hóa đường truyền dữ liệu để giảm độ trễ và bảo vệ origin server. Cuối cùng, câu chuyện vượt khó của Team VIB khi phát triển sản phẩm **UTMorpho trong 36 giờ** là một bài học thực tế đắt giá về việc giữ vững sự tập trung, tư duy module hóa mã nguồn và tối ưu hóa năng lực phối hợp của một đội ngũ lập trình.

---

## 7. Các bài học cốt lõi

- Việc cung cấp một **Ngữ cảnh (Context)** sạch, có cấu trúc vững chãi là điều kiện tiên quyết và quan trọng nhất để thu được các phản hồi đáng tin cậy từ LLM.
- Các công cụ AI đã chính thức bước qua giai đoạn chatbot sơ khai để đảm nhận các vai trò vận hành thực tế trong phân tích doanh nghiệp, tự động hóa workflow và chia sẻ dữ liệu phân tán.
- Áp dụng **Amazon CloudFront** mang lại cho đội ngũ kỹ sư một lá chắn tối ưu đầu tiên, giúp cải thiện vượt bậc tốc độ phản hồi toàn cầu, thắt chặt an ninh biên mạng và tiết kiệm ngân sách hạ tầng.
- Kỹ nghệ phát triển sản phẩm thần tốc đòi hỏi sự tập trung tuyệt đối vào việc giải quyết bài toán cốt lõi, ưu tiên các chu kỳ cải tiến liên tục thay vì sa đà vào việc thiết kế quá tải tính năng ở giai đoạn đầu.
- Lập trình viên cần có tư duy chủ động kiểm soát tính chất không xác định (**Non-deterministic**) của các mô hình AI để thiết kế nên các giải pháp tích hợp ổn định, nhất quán và an toàn cho người dùng.

---

## 8. Hình ảnh minh họa

Dưới đây là một số hình ảnh ghi nhận quá trình tham gia và theo dõi các phiên thảo luận kỹ thuật tại buổi Workshop:

![Tổng quan Sự kiện Tech Workshop](/FCAJ-Workshop-voquockhanh/images/workshop.jpg)
<i>Hình</i>
