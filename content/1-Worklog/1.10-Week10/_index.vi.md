---
title: "Worklog Tuần 10"
date: 2026-07-06
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

### Mục tiêu tuần 10:

* Trong tuần này, mục tiêu chính là hoàn thiện thiết kế kiến trúc tổng thể của dự án Retail Operations Monitoring Platform (ROMP) trên nền tảng AWS. Công việc tập trung vào việc nghiên cứu kiến trúc Serverless và Event-Driven, xác định vai trò của từng dịch vụ AWS, đồng thời xây dựng các sơ đồ kiến trúc nhằm mô tả rõ luồng xử lý và mối quan hệ giữa các thành phần trong hệ thống.

### Các công việc cần triển khai trong tuần này:

| Tuần | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 10 | Nghiên cứu yêu cầu nghiệp vụ của hệ thống giám sát hoạt động bán lẻ và xác định phạm vi dự án ROMP. | 06/07/2026 | 11/07/2026 |  |
| 10 | Tìm hiểu kiến trúc Serverless và Event-Driven Architecture trên AWS để lựa chọn mô hình triển khai phù hợp. | 06/07/2026 | 11/07/2026 |  |
| 10 | Nghiên cứu chức năng và vai trò của các dịch vụ AWS cốt lõi (AWS Lambda, Amazon EventBridge, Amazon CloudWatch). | 06/07/2026 | 11/07/2026 |  |
| 10 | Nghiên cứu các dịch vụ lưu trữ và gửi thông báo (Amazon DynamoDB, Amazon SES, AWS IAM). | 06/07/2026 | 11/07/2026 |  |
| 10  | Thiết kế kiến trúc tổng thể (High-Level Architecture - HLA) của hệ thống ROMP, mô tả tương tác giữa các thành phần. | 10/07/2026 | 11/07/2026 |  |
| 10  | Hoàn thiện tài liệu thiết kế kiến trúc, vẽ sơ đồ luồng dữ liệu (Data Flow Diagram) và tổng kết công việc tuần 10. | 06/07/2026 | 11/07/2026 |  |

### Kết quả đạt được tuần 10:

* Sau quá trình nghiên cứu và thiết kế, đã hoàn thành bộ sơ đồ kiến trúc của dự án ROMP, phản ánh đầy đủ cấu trúc hệ thống và quy trình xử lý dữ liệu.
* Lựa chọn thành công mô hình Serverless tích hợp Event-Driven giúp tối ưu chi phí vận hành và tính linh hoạt.
* Xác định rõ vai trò của từng dịch vụ AWS trong luồng xử lý: EventBridge kích hoạt định kỳ Lambda xử lý Business Rule & truy vấn Oracle DB Ghi log CloudWatch, lưu lịch sử vào DynamoDB và gửi email qua SES.
* Kiến trúc được xây dựng theo hướng tách biệt các thành phần, đảm bảo tính mở rộng, dễ bảo trì và tuân thủ các nguyên tắc của AWS Well-Architected Framework.