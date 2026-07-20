---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


# RETAIL OPERATIONS MONITORING PLATFORM (ROMP) WORKSHOP

#### Tổng quan

Retail Operations Monitoring Platform (ROMP) là giải pháp giám sát hoạt động bán lẻ theo thời gian thực hoạt động dựa trên kiến trúc AWS Serverless và mô hình hướng sự kiện (Event-Driven Architecture). ROMP đóng vai trò như một nền tảng kiểm soát độc lập, kết nối an toàn tới cơ sở dữ liệu Oracle hiện tại của doanh nghiệp theo chế độ chỉ đọc (Read-Only) để chủ động phân tích các Business Rule vận hành mà không gây ảnh hưởng hay làm gián đoạn hệ thống lõi (ERP/POS).

Trong bài lab này, chúng ta sẽ tiến hành xây dựng và cấu hình toàn bộ hạ tầng Serverless cho ROMP. Hệ thống sẽ tự động hóa quy trình quét dữ liệu, áp dụng các bộ quy tắc kinh doanh để phát hiện bất thường (như hàng hóa sắp hết hạn, cạn kiệt tồn kho, hoặc biến động doanh số), từ đó tự động lưu trữ lịch sử và phát ra cảnh báo tức thời tới quản trị viên.

**Kiến trúc các dịch vụ Serverless áp dụng
Workshop sẽ hướng dẫn bạn cách tích hợp và cấu hình chuỗi dịch vụ Cloud-Native dịch chuyển theo luồng sự kiện:**

* Amazon EventBridge: Đóng vai trò làm bộ lên lịch (Scheduler) tự động kích hoạt các tiến trình kiểm tra định kỳ.

* AWS Lambda: Trung tâm xử lý logic cốt lõi (Business Logic), được chia tách thành các module độc lập như Inventory, Expiry, Promotion, và Sales Monitoring nhằm tối ưu hóa khả năng bảo trì.

* Amazon DynamoDB: Cơ sở dữ liệu NoSQL Serverless dùng để lưu trữ và truy xuất toàn bộ lịch sử các cảnh báo được tạo ra.

* Amazon SES (Simple Email Service): Cơ chế chịu trách nhiệm gửi email thông báo tự động và tức thời đến các cấp quản lý khi phát hiện sự cố vận hành.

* Amazon CloudWatch: Hệ thống giám sát tập trung thu thập toàn bộ Log và Metrics, đảm bảo tính minh bạch và hỗ trợ phân tích lỗi hệ thống.

![ROMP Architecture](/images/2-Proposal/romp.jpg)

#### Nội dung

1. [Thiết lập nền tảng & Quyền IAM](5.1-Workshop-overview/)
2. [Khởi tạo Kho lưu trữ & Kênh thông báo (DynamoDB & SES)](5.2-Prerequiste/)
3. [Cấu hình Lambda và code Business Rule](5.3-S3-vpc/)
4. [CloudWatch với EventBridge](5.4-S3-onprem/)
5. [Kết quả đạt được ](5.5-Policy/)
6. [Dọn dẹp tài nguyên](5.6-Cleanup/)