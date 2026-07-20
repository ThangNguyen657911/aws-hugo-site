---
title: "Worklog Tuần 2"
date: 2026-05-04
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 2:

* Nắm vững kiến thức nền tảng và thực hành xây dựng hệ thống mạng ảo độc lập, an toàn trên AWS sử dụng dịch vụ Amazon VPC.
* Tìm hiểu, cài đặt và cấu hình AWS CLI để quản trị tài nguyên hệ thống trực tiếp từ dòng lệnh thay vì giao diện Console.
* Nghiên cứu dịch vụ quản lý DNS toàn cầu Amazon Route 53 và các mô hình kiến trúc phân giải tên miền kết hợp (Hybrid DNS) giữa môi trường On-Premises và AWS Cloud.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - **Kiến thức nền tảng Amazon VPC:** <br>&emsp; + Tìm hiểu mô hình phân chia dải mạng (CIDR, Subnets, Public/Private IP) <br>&emsp; + Tìm hiểu cơ chế định tuyến: Route Tables, Internet Gateway (IGW), NAT Gateway, NAT Instance | 11/05/2026   | 11/05/2026      | <https://docs.aws.amazon.com/> <br> <https://cloudjourney.awsstudygroup.com/> |
| 3   | - **Thực hành xây dựng VPC cơ bản:** <br>&emsp; + Khởi tạo VPC thủ công với đầy đủ các thành phần: Public Subnet, Private Subnet <br>&emsp; + Cấu hình Route Table và gán Internet Gateway để cho phép Public Subnet truy cập Internet <br>&emsp; + Cấu hình Security Group (kiểm soát traffic ở mức Instance) và Network ACL (kiểm soát ở mức Subnet) | 12/05/2026   | 12/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **AWS CLI (Command Line Interface):** <br>&emsp; + Tìm hiểu tổng quan và cách cài đặt AWS CLI trên hệ điều hành cá nhân <br>&emsp; + Cấu hình định danh bảo mật (`aws configure`) sử dụng Access Key / Secret Key của IAM User Admin <br>&emsp; + Thực hành một số tập lệnh cơ bản để truy vấn thông tin VPC, EC2 | 12/05/2026   | 12/06/2026      | <https://docs.aws.amazon.com/> |
| 5   | - **Amazon Route 53:** <br>&emsp; + Tìm hiểu các loại bản ghi DNS phổ biến (A, AAAA, CNAME, MX, TXT) <br>&emsp; + Khái niệm Hosted Zone (Public Hosted Zone và Private Hosted Zone) <br>&emsp; + Tìm hiểu về các chính sách định tuyến (Routing Policies): Simple, Weighted, Latency, Failover, Geolocation, Multi-value answer | 13/05/2026   | 13/05/2026      | <https://docs.aws.amazon.com/> |
| 6   | - **Hybrid DNS & Route 53 Resolver:** <br>&emsp; + Tìm hiểu thách thức khi phân giải tên miền giữa môi trường doanh nghiệp tự vận hành (On-Premises) và AWS <br>&emsp; + Nghiên cứu cơ chế hoạt động của Route 53 Resolver Inbound Endpoints và Outbound Endpoints cùng với Resolver Rules | 14/05/2026   | 14/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 7   | - **Thực hành Route 53 & Hybrid DNS:** <br>&emsp; + Cấu hình Private Hosted Zone trong VPC <br>&emsp; + Giả lập kịch bản phân giải DNS chéo bằng cách thiết lập Route 53 Resolver Rules và Endpoints hướng về một DNS Server tự dựng <br>&emsp; + Kiểm tra phân giải tên miền hai chiều thành công | 15/05/2026   | 15/05/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 2:

* **Về Amazon VPC:**
  * Hiểu sâu sắc cách AWS cô lập tài nguyên mạng của khách hàng. Phân biệt rõ ràng vai trò của **Public Subnet** (dành cho các dịch vụ cần giao tiếp trực tiếp với môi trường ngoài như Web Server) và **Private Subnet** (dành cho database, backend cần tính bảo mật cao).
  * Nắm vững cơ chế vận hành của **NAT Gateway** trong việc hỗ trợ các tài nguyên ở Private Subnet kết nối ra Internet để tải bản cập nhật nhưng không cho phép chiều ngược lại truy cập vào.
  * Phân biệt rõ hai lớp bảo mật mạng: **Security Group** (Stateful - tự động nhớ trạng thái kết nối) và **Network ACL** (Stateless - phải định nghĩa rõ ràng cả chiều vào và ra).

* **Về AWS CLI:**
  * Cài đặt thành công AWS CLI trên máy tính cá nhân và cấu hình kết nối an toàn bằng Profile riêng biệt thông qua Access Key / Secret Key được cấp phát từ tuần trước.
  * Sử dụng thành thạo các câu lệnh cơ bản để quản trị tài nguyên nhanh chóng mà không cần mở trình duyệt (ví dụ: `aws ec2 describe-vpcs`, `aws s3 ls`), hỗ trợ tối đa cho việc tự động hóa (automation scripts) sau này.

* **Về Amazon Route 53:**
  * Làm chủ các khái niệm DNS và cấu hình thành thạo **Public Hosted Zone** (phân giải tên miền ngoài Internet) và **Private Hosted Zone** (chỉ phân giải nội bộ trong phạm vi một hoặc nhiều VPC xác định).
  * Hiểu rõ cách áp dụng các Routing Policies linh hoạt dựa trên nhu cầu thực tế của hệ thống (như chuyển hướng lưu lượng dựa trên độ trễ của người dùng hoặc tự động chuyển hướng sang server dự phòng khi server chính gặp sự cố).

* **Về Hybrid DNS & Route 53 Resolver:**
  * Giải quyết triệt để bài toán kết nối DNS giữa môi trường đám mây và hạ tầng vật lý của doanh nghiệp thông qua **Route 53 Resolver**.
  * Hiểu rõ cơ chế hoạt động: **Inbound Endpoint** cho phép DNS Server ở On-Premises truy vấn các bản ghi nằm trong Private Hosted Zone của AWS; ngược lại, **Outbound Endpoint** kết hợp với **Resolver Rules** giúp chuyển tiếp các yêu cầu phân giải domain nội bộ của doanh nghiệp từ AWS ngược về On-Premises DNS Server.
  * Thực hành kiểm tra, debug và phân giải thành công tên miền chéo nội bộ mà không làm rò rỉ thông tin phân giải ra ngoài Internet công cộng.