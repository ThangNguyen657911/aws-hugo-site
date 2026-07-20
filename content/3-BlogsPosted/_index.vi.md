---
title: "Các bài blogs đã đăng"
date: 2026-04-27
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

{{% notice warning %}}  
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

Tại đây sẽ là phần liệt kê, giới thiệu các blogs mà các bạn đã đăng trên [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj):

###  [Blog 1 - Tối ưu hóa chi phí và độ tin cậy Big Data: Triển khai Remote Shuffle Service trên Amazon EMR với Apache Celeborn](3.1-Blog1/)
Blog này chia sẻ giải pháp tối ưu hóa chi phí và nâng cao độ tin cậy cho các hệ thống xử lý dữ liệu lớn (Apache Spark) trên AWS. Bằng cách tách biệt tài nguyên lưu trữ và tính toán qua việc triển khai Apache Celeborn làm Remote Shuffle Service (RSS), hệ thống có thể tự tin chạy 100% trên EC2 Spot Instances mà không lo ngại rủi ro mất dữ liệu shuffle khi node bị thu hồi.

###  [Blog 2 - Tự động hóa Patch Testing trên Amazon Redshift: Giải pháp bảo vệ Production Workloads tuyệt đối](3.2-Blog2/)
Blog này giới thiệu giải pháp xây dựng quy trình tự động hóa kiểm thử các bản vá (Patch Testing) trên Amazon Redshift. Giải pháp này giúp các doanh nghiệp mô phỏng và đánh giá tác động của các bản cập nhật hệ quản trị cơ sở dữ liệu trực tiếp trên bản sao của production workload, đảm bảo tính toàn vẹn và hiệu năng tối đa trước khi áp dụng thực tế.

###  [Blog 3 - Xây dựng Hệ thống Phát hiện Bất thường Thời gian thực quy mô lớn cùng Razorpay và Amazon MSK](3.3-Blog3/)
Blog này chia sẻ kiến trúc hệ thống ADA (Anomaly Detection and Alerting) của Razorpay được xây dựng trên Amazon MSK (Apache Kafka) và Apache Flink. Hệ thống giúp xử lý hơn 5 tỷ sự kiện mỗi ngày, phát hiện và ngăn chặn các hành vi gian lận tài chính theo thời gian thực dưới 30 giây, đồng thời tối ưu hóa tới 80% chi phí hạ tầng giám sát.