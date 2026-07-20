---
title: "Worklog Tuần 7"
date: 2026-06-08
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 7:

* Tìm hiểu và triển khai giải pháp bảo mật ứng dụng web chống lại các cuộc tấn công phổ biến với AWS WAF (Web Application Firewall).
* Nghiên cứu và xây dựng chính sách sao lưu, phục hồi dữ liệu tự động, tập trung thông qua AWS Backup.
* Tìm hiểu và thực hành các giải pháp kết nối mạng nâng cao giữa các VPC bằng cách sử dụng VPC Peering và AWS Transit Gateway.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - **AWS WAF (Web Application Firewall):** <br>&emsp; + Tìm hiểu lý thuyết về tường lửa ứng dụng web và danh sách lỗ hổng bảo mật phổ biến OWASP Top 10 <br>&emsp; + Tìm hiểu các khái niệm: Web ACL, Rules, Rule Groups, IP Sets | 14/06/2026   | 14/06/2026      | <https://docs.aws.amazon.com/> |
| 3   | - **Thực hành AWS WAF:** <br>&emsp; + Tạo Web ACL và cấu hình các AWS Managed Rules cơ bản <br>&emsp; + Thử nghiệm chặn truy cập dựa trên địa chỉ IP (IP Set) hoặc quốc gia (Geo-match) <br>&emsp; + Liên kết WAF với Application Load Balancer (ALB) hoặc CloudFront | 15/06/2026   | 15/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **AWS Backup:** <br>&emsp; + Nghiên cứu giải pháp sao lưu tập trung, tự động hóa và quản lý vòng đời dữ liệu (Lifecycle) trên AWS <br>&emsp; + Tìm hiểu các thành phần: Backup Vault, Backup Plan, Recovery Point | 16/06/2026   | 16/06/2026      | <https://docs.aws.amazon.com/> |
| 5   | - **Thực hành AWS Backup:** <br>&emsp; + Khởi tạo Backup Vault và thiết lập một Backup Plan tùy chỉnh <br>&emsp; + Cấu hình lịch sao lưu tự động và chính sách vòng đời (chuyển sang Cold Storage sau một khoảng thời gian) cho tài nguyên EC2 hoặc RDS | 17/06/2026   | 17/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **VPC Peering & AWS Transit Gateway (TGW):** <br>&emsp; + Nghiên cứu cách thiết lập kết nối mạng nội bộ giữa các VPC <br>&emsp; + So sánh ưu nhược điểm, cấu trúc mạng của kết nối dạng lưới (Mesh) VPC Peering truyền thống và mô hình hình sao (Hub-and-Spoke) của Transit Gateway | 18/06/2026   | 18/06/2026      | <https://docs.aws.amazon.com/> |
| 7   | - **Thực hành VPC Peering:** <br>&emsp; + Khởi tạo 2 VPC khác nhau, thiết lập kết nối VPC Peering Connection <br>&emsp; + Cấu hình lại Route Tables ở cả hai phía và kiểm tra kết nối thông qua việc ping/ssh giữa 2 EC2 instance nằm ở hai VPC riêng biệt | 19/06/2026   | 19/06/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 7:

* **Về AWS WAF (Web Application Firewall):**
  * Nắm vững cách thức AWS WAF hoạt động ở Layer 7 (Application Layer) trong mô hình OSI để lọc và ngăn chặn các mã độc hại, bảo vệ ứng dụng khỏi các lỗi bảo mật nguy hiểm như SQL Injection hay Cross-Site Scripting (XSS).
  * Thực hành cấu hình thành công một **Web ACL** có tích hợp sẵn các nhóm quy tắc được AWS quản lý (AWS Managed Rules), đồng thời thiết lập Custom Rule để chặn hoàn toàn một vài dải IP thử nghiệm. Đã liên kết Web ACL này với Application Load Balancer để trực tiếp bảo vệ hệ thống web nội bộ.

* **Về AWS Backup:**
  * Hiểu rõ tầm quan trọng của việc xây dựng chiến lược DR (Disaster Recovery) tự động hóa để đảm bảo tính sẵn sàng cao cho dữ liệu doanh nghiệp, thay vì thực hiện thủ công các thao tác tạo snapshot đơn lẻ.
  * Thiết lập thành công một **Backup Plan** tự động chạy định kỳ hằng ngày, lưu trữ bản sao lưu vào một **Backup Vault** bảo mật, đồng thời cấu hình Lifecycle giúp tự động chuyển các bản sao lưu cũ sang Cold Storage sau 30 ngày để tối ưu hóa chi phí lưu trữ.

* **Về VPC Peering & AWS Transit Gateway (TGW):**
  * Hiểu rõ logic định tuyến mạng trong AWS. Nắm chắc nguyên lý kết nối điểm-điểm không bắc cầu (non-transitive) của VPC Peering và cách giải quyết bài toán quản trị mạng quy mô lớn bằng Transit Gateway đóng vai trò như một bộ định tuyến trung tâm (cloud router).


  * Thực hiện kết nối thành công hai VPC riêng biệt bằng **VPC Peering**. Sau khi cập nhật chính xác Route Table của từng Subnet và cấu hình Security Group phù hợp, các máy chủ EC2 ở hai phân vùng mạng khác nhau đã có thể giao tiếp trực tiếp với nhau bằng địa chỉ IP nội bộ (Private IP) một cách an toàn mà không cần đi qua môi trường Internet công cộng.