---
title: "Worklog Tuần 4"
date: 2026-05-18
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 4:

* Tìm hiểu giải pháp di chuyển hệ thống ảo hóa cục bộ lên đám mây thông qua công cụ tự động hóa **VM Import/Export**.
* Nắm vững quy trình chuyển đổi cấu trúc cơ sở dữ liệu không đồng nhất (Heterogeneous Database Migration) sử dụng **AWS Schema Conversion Tool (SCT)**.
* Thực hành thiết lập và cấu hình **AWS Database Migration Service (DMS)** để di chuyển dữ liệu an toàn, liên tục và giảm thiểu tối đa thời gian gián đoạn của hệ thống (minimizing downtime).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - **AWS VM Import/Export (Lý thuyết & Chuẩn bị):** <br>&emsp; + Tìm hiểu khái niệm và kiến trúc chuyển đổi máy ảo (VM) từ môi trường On-Premises (VMware, Hyper-V) lên AWS EC2 <br>&emsp; + Tìm hiểu các định dạng đĩa ảo được hỗ trợ (OVA, VMDK, VHD) và cấu hình vai trò IAM Role (`vmimport`) | 24/05/2026   | 24/05/2026      | <https://docs.aws.amazon.com/> |
| 3   | - **Thực hành VM Import/Export:** <br>&emsp; + Tạo S3 Bucket và upload file đĩa ảo mẫu <br>&emsp; + Sử dụng AWS CLI thực thi lệnh `aws ec2 import-image` để chuyển đổi file đĩa ảo thành một Amazon Machine Image (AMI) hoạt động trên EC2 <br>&emsp; + Kiểm tra trạng thái import thông qua CLI | 25/05/2026   | 25/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **AWS Schema Conversion Tool (SCT) - Lý thuyết & Cài đặt:** <br>&emsp; + Tìm hiểu quy trình chuyển đổi Database Schema giữa các công nghệ khác nhau (ví dụ: Microsoft SQL Server sang Amazon Aurora/PostgreSQL) <br>&emsp; + Tải và cài đặt AWS SCT trên máy trạm cục bộ kèm theo các Database Drivers tương ứng | 26/05/2026   | 26/05/2026      | <https://docs.aws.amazon.com/> |
| 5   | - **Thực hành chuyển đổi Schema với SCT:** <br>&emsp; + Khởi tạo dự án trên AWS SCT, kết nối vào Database nguồn và đích <br>&emsp; + Chạy công cụ đánh giá (Assessment Report) để phân tích mức độ tương thích và các điểm cần tối ưu hóa thủ công <br>&emsp; + Thực hiện chuyển đổi và áp dụng Schema mới lên DB đích | 27/05/2026   | 27/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **AWS Database Migration Service (DMS) - Lý thuyết:** <br>&emsp; + Tìm hiểu kiến trúc tổng quan của AWS DMS gồm: Replication Instance, Source/Target Endpoints và Replication Tasks <br>&emsp; + Phân biệt các chế độ migration: Full Load, Full Load + CDC (Change Data Capture) và CDC-only | 28/05/2026   | 28/05/2026      | <https://docs.aws.amazon.com/> |
| 7   | - **Thực hành AWS DMS:** <br>&emsp; + Khởi tạo một Replication Instance và cấu hình kết nối Endpoint an toàn cho cả nguồn và đích <br>&emsp; + Tạo và kích hoạt một Database Migration Task (Full Load) để đồng bộ dữ liệu <br>&emsp; + Giám sát tiến độ dịch chuyển dữ liệu trực tiếp trên DMS Console | 29/05/2026   | 29/05/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 4:

* **Về VM Import/Export:**
  * Nắm vững quy trình dịch chuyển máy chủ vật lý hoặc máy ảo cục bộ lên nền tảng đám mây AWS một cách có hệ thống.
  * Thiết lập thành công IAM Role có tên `vmimport` với các chính sách (trust policy) chuẩn xác, cho phép dịch vụ truy cập vào S3 Bucket chứa file đĩa ảo.
  * Thực hành thành công việc import file ảnh đĩa ảo (Disk Image) từ Amazon S3 thành một **Amazon Machine Image (AMI)** bằng AWS CLI. Hiểu cách giám sát tiến trình chuyển đổi thông qua trạng thái `active`, `converting` và `completed`.

* **Về AWS Schema Conversion Tool (SCT):**
  * Hiểu rõ vai trò quan trọng của SCT trong các dự án dịch chuyển cơ sở dữ liệu không đồng nhất (khác biệt về mặt kiến trúc engine).
  * Cài đặt thành công ứng dụng AWS SCT kết hợp với cấu hình các thư viện Driver liên kết (JDBC Drivers).
  * Tạo thành công một **Database Migration Assessment Report** dưới dạng PDF. Báo cáo này giúp nhận diện rõ các thành phần không thể tự động chuyển đổi (chẳng hạn các Stored Procedures hay Triggers phức tạp), từ đó ước lượng chính xác khối lượng công việc cần can thiệp thủ công.
  * Thực hiện convert thành công các cấu trúc bảng (Tables), ràng buộc (Constraints) và index từ cơ sở dữ liệu nguồn sang cơ sở dữ liệu đích mẫu.

* **Về AWS Database Migration Service (DMS):**
  * Làm chủ các thành phần cốt lõi của kiến trúc AWS DMS bao gồm: Máy chủ xử lý trung gian (**Replication Instance**), các điểm kết nối đầu cuối (**Source/Target Endpoints**) và tác vụ điều phối luồng dữ liệu (**Replication Tasks**).
  * Cấu hình và kết nối thành công hai Endpoint kiểm thử thông qua cơ chế kiểm tra kết nối (Run Connection Test) đạt trạng thái `successful`.
  * Thực thi thành công một tác vụ chuyển dịch dữ liệu theo chế độ **Full Load**, kiểm tra tính toàn vẹn của dữ liệu sau khi di chuyển trên Database đích và biết cách cấu hình tính năng **CDC (Change Data Capture)** để liên tục đồng bộ các thay đổi phát sinh từ cơ sở dữ liệu nguồn trong thời gian thực mà không làm gián đoạn hệ thống đang vận hành.