---
title: "Worklog Tuần 9"
date: 2026-06-22
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 9:

* Nghiên cứu giải pháp lưu trữ tệp tin hiệu năng cao, tương thích hoàn toàn với các hệ thống tệp phổ biến thông qua Amazon FSx.
* Tìm hiểu và triển khai cơ sở dữ liệu NoSQL quy mô lớn, độ trễ cực thấp với Amazon DynamoDB, đồng thời nắm bắt các cơ chế tối ưu hóa chi phí dài hạn với AWS Savings Plans.
* Khám phá bộ đôi dịch vụ phân tích dữ liệu phi cấu trúc và bán cấu trúc mạnh mẽ: AWS Glue (ETL pipeline) và Amazon Athena (truy vấn không máy chủ bằng SQL chuẩn).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - **Amazon FSx:** <br>&emsp; + Tìm hiểu lý thuyết về Amazon FSx và các biến thể hệ thống tệp phổ biến (FSx for Windows File Server, FSx for Lustre, FSx for NetApp ONTAP) <br>&emsp; + So sánh sự khác biệt về hiệu năng và kịch bản sử dụng giữa Amazon EFS và Amazon FSx | 28/06/2026   | 28/06/2026      | <https://docs.aws.amazon.com/> |
| 3   | - **Thực hành Amazon FSx & DynamoDB:** <br>&emsp; + Khởi tạo và cấu hình một hệ thống tệp Amazon FSx for Windows File Server, thực hiện kết nối (mount) từ một máy chủ EC2 Windows <br>&emsp; + Tìm hiểu lý thuyết về Amazon DynamoDB: khái niệm Partition Key, Sort Key, và cơ chế Read/Write Capacity Modes (On-Demand vs Provisioned) | 29/06/2026   | 29/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Thực hành Amazon DynamoDB & AWS Savings Plans:** <br>&emsp; + Khởi tạo một DynamoDB Table, thực hiện các thao tác CRUD cơ bản (thêm, đọc, sửa, xóa dữ liệu) thông qua AWS Console và CLI <br>&emsp; + Nghiên cứu cơ chế tối ưu hóa chi phí với AWS Savings Plans: So sánh Compute Savings Plans, EC2 Instance Savings Plans và SageMaker Savings Plans | 30/06/2026   | 30/06/2026      | <https://docs.aws.amazon.com/> |
| 5   | - **AWS Glue:** <br>&emsp; + Tìm hiểu kiến trúc của AWS Glue: Data Catalog, Crawlers, Connection, và Glue ETL Jobs <br>&emsp; + Nghiên cứu cách AWS Glue tự động khám phá dữ liệu, trích xuất lược đồ (schema) và chuyển đổi định dạng dữ liệu (ví dụ: CSV sang Parquet) | 01/07/2026   | 01/07/2026      | <https://docs.aws.amazon.com/> |
| 6   | - **Amazon Athena:** <br>&emsp; + Tìm hiểu nguyên lý hoạt động của Amazon Athena - giải pháp truy vấn dữ liệu trực tiếp trên Amazon S3 bằng SQL chuẩn mà không cần quản lý hạ tầng <br>&emsp; + Nghiên cứu các phương pháp tối ưu hiệu năng và giảm chi phí truy vấn (phân vùng dữ liệu - Partitioning, nén dữ liệu, sử dụng định dạng cột Parquet/ORC) | 02/07/2026   | 02/07/2026      | <https://docs.aws.amazon.com/> |
| 7   | - **Thực hành Tích hợp AWS Glue & Amazon Athena:** <br>&emsp; + Thiết lập một Glue Crawler để quét tập dữ liệu thô (dạng CSV) lưu trữ trên Amazon S3 và tự động tạo bảng trong Glue Data Catalog <br>&emsp; + Sử dụng Amazon Athena để thực hiện các câu lệnh SQL truy vấn trực tiếp trên bảng vừa được định nghĩa trong Data Catalog | 03/07/2026   | 03/07/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 9:

* **Về Amazon FSx:**
  * Nắm vững các kịch bản thực tế khi lựa chọn giải pháp lưu trữ: sử dụng *FSx for Windows File Server* cho các ứng dụng Windows bản địa tích hợp Active Directory, và *FSx for Lustre* cho các tác vụ tính toán hiệu năng cao (HPC), học máy cần thông lượng cực lớn.
  * Triển khai thành công một hệ thống tệp FSx Windows, liên kết hoạt động mượt mà với máy chủ EC2 và hiểu rõ cơ chế phân quyền bảo mật cấp tệp tin (NTFS permissions).

* **Về Amazon DynamoDB & Savings Plans:**
  * Hiểu rõ cơ chế phân tán dữ liệu của DynamoDB dựa trên Partition Key, cách thiết lập các chỉ mục phụ (Local Secondary Index - LSI, Global Secondary Index - GSI) để tối ưu hóa hiệu năng truy vấn cho các bài toán thực tế.
  * Biết cách sử dụng công cụ *AWS Cost Explorer* để phân tích mức độ sử dụng tài nguyên liên tục, từ đó đưa ra đề xuất mua gói *Savings Plans* phù hợp (tiết kiệm lên đến 72% chi phí so với giá On-Demand) dựa trên cam kết sử dụng tài nguyên ổn định theo giờ trong thời hạn 1 hoặc 3 năm.

* **Về AWS Glue & Amazon Athena:**
  * Nắm vững quy trình xử lý dữ liệu hiện đại (Serverless Analytics Pipeline). Hiểu rõ vai trò của *AWS Glue Data Catalog* như một siêu kho dữ liệu (metadata repository) tập trung giúp quản lý cấu trúc dữ liệu trên Cloud.
  * Thiết lập và vận hành thành công một luồng phân tích dữ liệu khép kín: Sử dụng **Glue Crawler** tự động phân tích và trích xuất cấu trúc dữ liệu từ tệp tin CSV lưu trên S3, sau đó dùng **Amazon Athena** viết các câu lệnh truy vấn SQL phức tạp (SELECT, WHERE, GROUP BY) để phân tích dữ liệu trực tiếp với tốc độ phản hồi tính bằng mili-giây mà không cần khởi tạo bất kỳ máy chủ cơ sở dữ liệu nào.