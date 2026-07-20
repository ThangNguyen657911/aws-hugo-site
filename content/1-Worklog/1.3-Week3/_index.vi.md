---
title: "Worklog Tuần 3"
date: 2026-05-11
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 3:

* Tìm hiểu và thực hành quản trị máy chủ EC2 an toàn, không cần mở cổng bảo mật hoặc sử dụng SSH Key thông qua **AWS Systems Manager (SSM)** và **Session Manager**.
* Nắm vững giải pháp giám sát hệ thống với **AWS CloudWatch**, biết cách cấu hình cảnh báo tự động khi tài nguyên quá tải và trực quan hóa dữ liệu giám sát.
* Tiếp cận phương pháp quản lý hạ tầng bằng mã nguồn (Infrastructure as Code - IaC) thông qua dịch vụ **AWS CloudFormation** để tự động hóa việc khởi tạo tài nguyên.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - **AWS Systems Manager & Session Manager (Lý thuyết):** <br>&emsp; + Tìm hiểu tổng quan về AWS Systems Manager (SSM) và cơ chế quản lý máy chủ tập trung <br>&emsp; + Tìm hiểu Session Manager: Cách kết nối terminal an toàn vào EC2 mà không cần mở port 22 (SSH), không cần Bastion Host hay quản lý SSH Keys | 17/05/2026   | 17/05/2026      | <https://docs.aws.amazon.com/> |
| 3   | - **Thực hành SSM & Session Manager:** <br>&emsp; + Tạo IAM Role với policy `AmazonSSMManagedInstanceCore` gán cho EC2 <br>&emsp; + Khởi chạy EC2 Instance đã cài sẵn SSM Agent và thực hiện kết nối shell an toàn thông qua Session Manager trên AWS Console | 18/05/2026   | 18/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **AWS CloudWatch (Lý thuyết):** <br>&emsp; + Nghiên cứu các thành phần chính của CloudWatch: Metrics (Chỉ số), Logs (Nhật ký), Alarms (Cảnh báo) và Dashboards (Bảng điều khiển) <br>&emsp; + Phân biệt sự khác nhau giữa giám sát cơ bản (Basic Monitoring) và giám sát chi tiết (Detailed Monitoring) | 19/05/2026   | 19/05/2026      | <https://docs.aws.amazon.com/> |
| 5   | - **Thực hành CloudWatch Monitoring & Alarms:** <br>&emsp; + Cài đặt CloudWatch Agent lên EC2 để thu thập log hệ thống và RAM metrics <br>&emsp; + Thiết lập CloudWatch Alarms kết hợp Amazon SNS để gửi email cảnh báo tự động khi CPU vượt quá 80% <br>&emsp; + Thiết lập Dashboard trực quan theo dõi tài nguyên | 20/05/2026   | 20/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **AWS CloudFormation (Lý thuyết):** <br>&emsp; + Tìm hiểu khái niệm Infrastructure as Code (IaC) và lợi ích của việc tự động hóa hạ tầng <br>&emsp; + Phân tích cấu trúc file template CloudFormation (YAML/JSON) gồm các phần: Parameters, Resources, Outputs | 21/05/2026   | 21/05/2026      | <https://docs.aws.amazon.com/> |
| 7   | - **Thực hành CloudFormation:** <br>&emsp; + Soạn thảo template YAML cơ bản để triển khai tự động một tài nguyên EC2 nằm trong một Security Group riêng biệt <br>&emsp; + Thực thi tạo, cập nhật (Update) và xóa (Delete) Stack trên giao diện CloudFormation để hiểu cơ chế rollback | 22/05/2026   | 22/05/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 3:

* **Về AWS Systems Manager & Session Manager:**
  * Hiểu rõ cơ chế hoạt động của SSM Agent chạy ngầm trên máy chủ, giúp AWS quản lý hệ điều hành từ xa một cách an toàn thông qua các API nội bộ của AWS thay vì phơi bày cổng mạng ra Internet công cộng.
  * Thực hành kết nối trực tiếp vào dòng lệnh (shell) của EC2 trực tiếp trên trình duyệt bằng **Session Manager** mà không cần cấu hình Public IP, không cần mở cổng 22 (SSH) trên Security Group và hoàn toàn loại bỏ việc quản lý file key pair (.pem), giúp giảm thiểu tối đa diện tích tấn công (attack surface) của hệ thống.

* **Về AWS CloudWatch:**
  * Nắm vững cách CloudWatch thu thập metrics từ các dịch vụ AWS theo chu kỳ mặc định (5 phút đối với basic) hoặc chuyên sâu (1 phút đối với detailed).
  * Cài đặt thành công **CloudWatch Agent** lên EC2 để thu thập các chỉ số mà hypervisor mặc định không đọc được (như dung lượng bộ nhớ RAM đang sử dụng, dung lượng ổ đĩa khả dụng) và đồng bộ về CloudWatch console.
  * Cấu hình thành công hệ thống cảnh báo tự động: Khi kiểm thử giả lập tải CPU tăng cao (stress-test), hệ thống phát hiện vượt ngưỡng cấu hình và tự động kích hoạt CloudWatch Alarm, gửi thành công email thông báo trạng thái `ALARM` tới quản trị viên thông qua dịch vụ **Amazon SNS (Simple Notification Service)**.
  * Thiết kế được một màn hình **CloudWatch Dashboard** trực quan hiển thị biểu đồ CPU, RAM và Disk Space của máy chủ theo thời gian thực.

* **Về AWS CloudFormation:**
  * Hiểu rõ tư duy triển khai hạ tầng dưới dạng mã nguồn (IaC). Biết cách viết và đóng gói hạ tầng vào một file template duy nhất để dễ dàng tái bản môi trường (Dev, Staging, Production) một cách nhất quán và chính xác.
  * Đọc hiểu và tự tay viết được template định dạng **YAML** khai báo các thuộc tính đầu vào (Parameters), định nghĩa tài nguyên cần khởi tạo (Resources) và xuất ra các thông tin quan trọng như ID hay Public DNS của EC2 ở phần đầu ra (Outputs).
  * Làm quen với vòng đời của Stack (Stack Lifecycle): Hiểu rõ cách CloudFormation xử lý lỗi (nếu một tài nguyên trong Stack khởi tạo lỗi, hệ thống sẽ tự động thực hiện quá trình `Rollback` để xóa bỏ các tài nguyên đã tạo trước đó, đưa hệ thống về trạng thái an toàn ban đầu).