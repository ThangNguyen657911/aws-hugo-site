---
title: "Blog 3"
date: 2024-01-03
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# XÂY DỰNG HỆ THỐNG PHÁT HIỆN BẤT THƯỜNG THỜI GIAN THỰC QUY MÔ LỚN CÙNG RAZORPAY VÀ AMAZON MSK

! Khi vận hành các hệ thống tài chính - thanh toán quy mô lớn, mỗi giây phát hiện chậm trễ các hành vi bất thường (anomaly) đồng nghĩa với việc giao dịch thất bại, doanh thu bị mất và niềm tin của khách hàng bị xói mòn. 

Hôm nay, mình xin chia sẻ kiến trúc hệ thống **ADA (Anomaly Detection and Alerting)** – nền tảng phát hiện bất thường và ngăn ngừa gian lận theo thời gian thực của Razorpay (một trong những Fintech lớn nhất Ấn Độ) được xây dựng trên nền tảng **Amazon Managed Streaming for Apache Kafka (Amazon MSK)** và **Apache Flink**. Hệ thống này giúp Razorpay xử lý hơn 5 tỷ event mỗi ngày, phát hiện sự cố trong dưới 30 giây và cắt giảm tới 80% chi phí giám sát.

---

## Bài toán: Khi các ngưỡng tĩnh (Static Thresholds) sụp đổ trước quy mô lớn

Trước khi xây dựng ADA, hệ thống giám sát cũ của Razorpay (dựa trên Pinot + ThirdEye) đã chạm ngưỡng giới hạn khi công ty tăng trưởng mạnh mẽ, đạt mốc hơn 500 triệu giao dịch/tháng:

* **Điểm mù giám sát:** Các sự cố suy giảm hệ thống hoặc tụt tỷ lệ thành công (Success Rate) chỉ được phát hiện khi khách hàng phàn nàn. Khi vận hành thủ công, hàng ngàn giao dịch đã thất bại trước khi con người kịp nhận ra.
* **Gian lận tốc độ cao (Fraud at velocity):** Các cuộc tấn công thử thẻ (card-testing), lạm dụng hạn mức đòi hỏi phải được phát hiện dưới 1 phút, điều mà hệ thống xử lý theo mẻ (batch) truyền thống hoàn toàn bất lực.
* **Bão cảnh báo (Alert Fatigue):** Việc cấu hình các ngưỡng cố định (static thresholds) tạo ra tình thế tiến thoái lưỡng nan: Đặt quá chặt thì ngập trong cảnh báo giả, đặt quá lỏng thì bỏ sót các cuộc tấn công thực tế.
* **Chi phí tỷ lệ thuận với độ phức tạp (High Cardinality):** Giám sát riêng lẻ cho hàng ngàn đối tác (merchants) tiêu tốn tới $500K/năm kèm theo độ trễ truy vấn (SLA) tối thiểu từ 1–2 phút, hoàn toàn không thể mở rộng.

---

## Kiến trúc ADA: Amazon MSK đóng vai trò Xương sống luồng dữ liệu (Streaming Backbone)

Để giải quyết triệt để các hạn chế trên, Razorpay đã tái cấu trúc toàn diện hệ thống với mô hình **Decoupled Data Pipeline**, đặt **Amazon MSK** làm trung tâm điều phối dữ liệu.

![Blog3](/images/blog3.jpg)

Kiến trúc này vận hành dựa trên các thành phần cốt lõi sau:

### 1. Ingestion Layer hiệu năng cao với Amazon MSK
* **Toàn bộ sự kiện thay đổi dữ liệu (CDC)** từ các database core (Amazon Aurora MySQL) thông qua Debezium cùng các event từ ứng dụng được đẩy trực tiếp vào các Kafka topic do Amazon MSK quản lý.
* **Phân vùng theo Tenant (Tenant-partitioned topics):** Dữ liệu của các khối doanh nghiệp (Payments, Payroll, Banking) được cô lập logic trên các topic riêng nhưng chia sẻ chung hạ tầng vật lý của cụm MSK, đảm bảo SLA băng thông độc lập và tối ưu chi phí.
* **Đảm bảo độ tin cậy tuyệt đối:** Cụm MSK được triển khai phân tán trên 3 Availability Zones (AZs) với cấu hình bền vững dữ liệu cao: `replication.factor=3`, `min.insync.replicas=2`, và phía producer sử dụng `acks=all`. Rủi ro mất mát dữ liệu hoặc gián đoạn luồng ingestion khi có broker gặp sự cố bằng cấu hình này được triệt tiêu hoàn toàn.

### 2. Xử lý luồng trạng thái (Stateful Stream Processing) với Apache Flink
Apache Flink đóng vai trò là engine tính toán trung gian, liên tục tiêu thụ dữ liệu từ MSK với ngữ nghĩa exactly-once. Quy trình xử lý gồm 5 giai đoạn cốt lõi:
* **Kafka Source:** Tiếp nhận luồng dữ liệu thô từ MSK.
* **Watermarking:** Xử lý các sự kiện đến muộn (late-arriving events) với khả năng dung lỗi gấp 2 lần kích thước window.
* **Windowed Aggregation:** Gom cụm dữ liệu theo từng Merchant và tính toán nhanh các chỉ số (tỷ lệ thành công, độ trễ, volume).
* **Async I/O Lookup:** Thực hiện các truy vấn phi bất đồng bộ (hỗ trợ tới 1.024 kết nối đồng thời) sang ClickHouse để lấy các dữ liệu Baseline chuẩn đã tính toán từ trước.
* **Rule Evaluation:** Đối chiếu dữ liệu real-time với Baseline bằng các thuật toán máy học hoặc Complex Event Processing (Flink CEP) nhằm phát hiện ngay lập tức các chuỗi hành vi gian lận (ví dụ: 5 lần decline liên tiếp theo sau bởi 1 lần success).

### 3. Tách biệt Logic kiểm tra bằng ngôn ngữ AdaDSL
Điểm đắt giá nhất của ADA là việc tách biệt hoàn toàn giữa **Định nghĩa luật (Rule definition)** và **Thực thi hạ tầng (Execution)**. Razorpay phát triển ngôn ngữ mã nguồn khai báo AdaDSL dạng mã con người có thể đọc hiểu.
* Khi các chuyên gia vận hành cập nhật một rule mới, định nghĩa này được serialize và đẩy vào một Kafka snapshot topic riêng trên MSK.
* Flink sẽ tiêu thụ topic này dưới dạng một **Broadcast Stream**, tự động áp dụng logic mới vào toàn bộ các luồng pipeline đang chạy ngay lập tức (**Hot-reload**) mà không cần phải restart hệ thống hay redeploy code.

---

## Kết quả đột phá và Bài học kinh nghiệm

Nền tảng ADA chạy trên Amazon MSK đã đem lại những cải tiến vượt trội về mặt vận hành cho Razorpay:

* **Giảm 80%** chi phí hạ tầng so với kiến trúc cũ.
* Độ trễ phát hiện bất thường giảm từ vài phút xuống **dưới 30 giây**.
* **Giảm 90%** số lượng cảnh báo giả nhờ các baseline động có khả năng thích ứng theo lịch trình, ngày lễ, khung giờ (Calendar-aware patterns).
* Duy trì cam kết **99.99% Uptime** cho toàn bộ hệ thống giám sát.

---

## Kết luận

**Key Takeaway cho Kỹ sư Hệ thống:** Đối với các hệ thống xử lý giao dịch tần suất cao, việc đầu tư vào một xương sống streaming vững chắc như Amazon MSK ngay từ đầu không chỉ là giải pháp tối ưu hóa, mà là điều kiện tiên quyết để vận hành ổn định. Việc decoupling hoàn toàn giữa bên sản xuất sự kiện và bên tiêu thụ xử lý giúp bạn tự do mở rộng, tùy biến tính năng (như tích hợp thêm các model ML dự báo, LLM hỗ trợ phân tích nguyên nhân gốc rễ RCA) mà không làm ảnh hưởng đến luồng thanh toán chính của khách hàng.

Tham khảo nguồn tại: [aws.amazon.com/vi/blogs/big-data/how-razorpay-built-real-time-anomaly-detection-with-amazon-msk](https://aws.amazon.com/vi/blogs/big-data/how-razorpay-built-real-time-anomaly-detection-with-amazon-msk/).

Mọi người nghĩ sao về mô hình phát hiện bất thường thời gian thực này của Razorpay? Cùng để lại bình luận và thảo luận bên dưới nhé!