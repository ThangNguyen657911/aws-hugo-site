---
title: "Worklog Tuần 11"
date: 2026-07-13
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

### Mục tiêu tuần 11:

* Trong tuần này, mục tiêu chính là bắt đầu triển khai hệ thống Retail Operations Monitoring Platform (ROMP) trên nền tảng AWS dựa trên kiến trúc đã được thiết kế ở các tuần trước. Đồng thời, tiến hành xây dựng môi trường phát triển, cấu hình các dịch vụ AWS và phát triển module giám sát đầu tiên của hệ thống (Inventory Monitoring).

### Các công việc cần triển khai trong tuần này:

| Tuần | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 11 | Khởi tạo dự án ROMP, thiết lập cấu trúc thư mục (Layered Architecture), môi trường Virtual Environment (`.venv`) và cài đặt các thư viện Python (`boto3`, `oracledb`, `python-dotenv`). | 13/07/2026 | 18/07/2026 | |
| 11 | Cấu hình kết nối cơ sở dữ liệu Oracle ở chế độ Read Only phục vụ việc truy xuất dữ liệu an toàn. | 13/07/2026 | 18/07/2026 | |
| 11 | Thiết lập các dịch vụ AWS nền tảng: Cấu hình IAM Role (Least Privilege), tạo bảng Amazon DynamoDB lưu lịch sử cảnh báo và xác thực Amazon SES để gửi mail thông báo. | 13/07/2026 | 18/07/2026 | |
| 11 | Xây dựng mã nguồn AWS Lambda cho module Inventory Monitoring (`config`, `logger`, `oracle_service`, `inventory_repository`, `inventory_service`, `handler`, `lambda_function`). | 13/07/2026 | 18/07/2026 | |
| 11 | Xây dựng Business Rule kiểm tra lượng tồn kho (`quantity`) và phân loại trạng thái sản phẩm: Normal, Low Stock, Out of Stock. | 13/07/2026 | 18/07/2026 | |
| 11 | Cấu hình Amazon EventBridge kích hoạt Lambda theo lịch định kỳ; tiến hành kiểm thử toàn trình (End-to-End Test) và theo dõi log thực thi trên Amazon CloudWatch. | 13/07/2026 | 18/07/2026 | |

### Kết quả đạt được tuần 11:

* Triển khai thành công module **Inventory Monitoring** của hệ thống ROMP trên nền tảng AWS hoạt động ổn định và chính xác theo kiến trúc đề ra.
* Hoàn thiện luồng tự động hóa khép kín: Amazon EventBridge kích hoạt định kỳ AWS Lambda truy vấn Oracle Database Xử lý Business Rule phát hiện tồn kho thấp/hết hàng.
* Tích hợp thành công các dịch vụ hạ tầng AWS: Gửi email cảnh báo qua Amazon SES, lưu trữ dữ liệu lịch sử cảnh báo vào Amazon DynamoDB và ghi log vận hành trên Amazon CloudWatch.
* Đảm bảo tính an toàn và nguyên tắc quản trị hệ thống bằng việc cấu hình IAM Role theo nguyên tắc Least Privilege và kết nối Oracle Database ở chế độ Read Only.