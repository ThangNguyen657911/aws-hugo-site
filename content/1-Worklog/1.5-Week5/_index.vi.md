---
title: "Worklog Tuần 5"
date: 2026-05-25
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 5:

* Tìm hiểu và ứng dụng mô hình điện toán không máy chủ (Serverless) với **AWS Lambda** để tự động hóa các tác vụ quản trị hệ thống theo điều kiện hoặc lịch trình.
* Nghiên cứu giải pháp trực quan hóa dữ liệu giám sát nâng cao bằng cách tích hợp **Grafana** với các nguồn dữ liệu từ AWS (như CloudWatch).
* Nắm vững chiến lược phân loại, quản lý tài nguyên tập trung quy mô lớn thông qua **AWS Tagging Best Practices** và **AWS Resource Groups**.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - **AWS Lambda Automation (Lý thuyết):** <br>&emsp; + Khái niệm điện toán Serverless và cách hoạt động của AWS Lambda <br>&emsp; + Tìm hiểu mô hình lập trình hướng sự kiện (Event-driven) và cách Lambda tích hợp với Amazon EventBridge (CloudWatch Events) để chạy tự động theo lịch trình | 31/05/2026   | 31/05/2026      | <https://docs.aws.amazon.com/> |
| 3   | - **Thực hành AWS Lambda Automation:** <br>&emsp; + Viết một hàm Lambda đơn giản bằng Python (sử dụng thư viện `boto3`) để tự động tắt các EC2 Instance không sử dụng vào cuối ngày nhằm tiết kiệm chi phí <br>&emsp; + Cấu hình EventBridge Rule làm trigger kích hoạt Lambda định kỳ | 1/06/2026   | 01/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Grafana (Lý thuyết & Thiết lập):** <br>&emsp; + Tìm hiểu tổng quan về Grafana và ưu thế trực quan hóa dữ liệu so với CloudWatch Dashboard mặc định <br>&emsp; + Nghiên cứu các phương án triển khai Grafana (tự cài đặt trên EC2 hoặc sử dụng dịch vụ Amazon Managed Grafana) | 02/06/2026   | 02/06/2026      | <https://docs.aws.amazon.com/> |
| 5   | - **Thực hành Tích hợp Grafana & CloudWatch:** <br>&emsp; + Cấu hình IAM Role/Policy cho phép Grafana đọc dữ liệu từ CloudWatch <br>&emsp; + Thêm CloudWatch làm Data Source trên Grafana và thiết kế một Dashboard giám sát hiệu năng EC2 chuyên nghiệp với các biểu đồ tùy biến sâu | 03/06/2026   | 03/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **AWS Tagging & Resource Groups (Lý thuyết):** <br>&emsp; + Tìm hiểu quy chuẩn đặt nhãn (Tagging Best Practices) phục vụ cho việc quản lý chi phí, phân quyền bảo mật (ABAC) và vận hành hệ thống <br>&emsp; + Tìm hiểu về AWS Resource Groups để gom nhóm tài nguyên theo dự án/môi trường | 04/06/2026   | 04/06/2026      | <https://docs.aws.amazon.com/> |
| 7   | - **Thực hành Quản lý Tài nguyên với Tagging & Resource Groups:** <br>&emsp; + Sử dụng công cụ Tag Editor để gắn thẻ hàng loạt cho các tài nguyên đang hoạt động <br>&emsp; + Khởi tạo một Resource Group dựa trên tag (Query-based) để quản lý tập trung và theo dõi trạng thái của toàn bộ tài nguyên thuộc một dự án cụ thể | 05/06/2026   | 05/06/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 5:

* **Về AWS Lambda Automation:**
  * Hiểu sâu sắc về mô hình Serverless, giúp loại bỏ hoàn toàn gánh nặng quản lý, vá lỗi hệ điều hành và tự động tối ưu hóa tài nguyên tính toán theo nhu cầu thực tế.
  * Viết và triển khai thành công một hàm Python sử dụng thư viện **Boto3 SDK** để tự động kiểm tra trạng thái và dừng các EC2 Instance có gắn thẻ `Environment: Development` vào lúc 19:00 hàng ngày.
  * Liên kết thành công hàm Lambda với **Amazon EventBridge Rule** (sử dụng Cron expression), giúp hệ thống tự động vận hành mà không cần can thiệp thủ công, tối ưu hóa đến 30% chi phí chạy máy chủ thử nghiệm ngoài giờ làm việc.

* **Về Grafana:**
  * Đánh giá được sự linh hoạt của Grafana trong việc hợp nhất, trực quan hóa và truy vấn dữ liệu từ nhiều nguồn khác nhau trên một giao diện Dashboard duy nhất.
  * Thiết lập thành công kết nối bảo mật giữa Grafana và AWS bằng cách phân quyền IAM Role hạn chế (chỉ cho phép đọc dữ liệu giám sát CloudWatch - `CloudWatchReadOnlyAccess`).
  * Xây dựng thành công một **Grafana Dashboard** hoàn chỉnh, trực quan hóa sinh động các chỉ số của EC2 (CPU Utilization, Network In/Out, Disk Read/Write) với các ngưỡng cảnh báo màu sắc rõ ràng, dễ dàng theo dõi hơn so với giao diện mặc định.

* **Về AWS Tagging & Resource Groups:**
  * Xây dựng được bộ quy chuẩn đặt tên nhãn (Tagging Schema) chuẩn hóa cho môi trường thực tập, bao gồm các tag bắt buộc như: `Project`, `Environment`, `Owner` và `CostCenter`.
  * Sử dụng thành công công cụ **Tag Editor** trong AWS Resource Groups để tìm kiếm nhanh và sửa đổi/bổ sung tag đồng loạt cho hàng loạt tài nguyên (EC2, S3, RDS, Security Groups) bị thiếu tag từ trước.
  * Khởi tạo thành công một **Query-based Resource Group** gom nhóm toàn bộ các tài nguyên có chung tag `Project: FirstCloudAI`. Từ Resource Groups console, có thể dễ dàng giám sát trạng thái hoạt động, cấu hình và xem nhanh các cảnh báo CloudWatch Alarm liên quan đến dự án này mà không cần truy cập riêng lẻ từng dịch vụ.