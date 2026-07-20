---
title: "Worklog Tuần 8"
date: 2026-06-15
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 8:

* Tìm hiểu công nghệ container hóa với Docker, cách xây dựng tối ưu hóa Dockerfile và quản lý vòng đời ứng dụng container.
* Nghiên cứu giải pháp điều phối container với Amazon ECS (Elastic Container Service) chạy trên môi trường không máy chủ AWS Fargate.
* Xây dựng luồng tích hợp và triển khai liên tục (CI/CD) tự động hóa hoàn toàn với AWS CodePipeline.
* Tìm hiểu cơ chế tích hợp lưu trữ lai (Hybrid Cloud Storage) giữa hạ tầng On-Premises và AWS thông qua AWS Storage Gateway.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - **Docker & Containerization:** <br>&emsp; + Tìm hiểu lý thuyết về Container, sự khác biệt giữa Virtual Machine (VM) và Container <br>&emsp; + Các lệnh Docker cơ bản: build, run, push/pull, volume, network | 21/06/2026   | 21/06/2026      | <https://docs.docker.com/> |
| 3   | - **Thực hành Docker & AWS ECR:** <br>&emsp; + Viết Dockerfile đóng gói một ứng dụng web đơn giản (Node.js/Python) <br>&emsp; + Khởi tạo kho chứa Private Repository trên Amazon ECR (Elastic Container Registry) <br>&emsp; + Đẩy (Push) Docker image lên Amazon ECR | 22/06/2026   | 22/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Amazon ECS & AWS Fargate:** <br>&emsp; + Nghiên cứu kiến trúc Amazon ECS và các khái niệm cốt lõi: Task Definition, Task, Service, Cluster <br>&emsp; + Phân biệt cơ chế chạy ECS trên EC2 và Serverless với AWS Fargate | 23/06/2026   | 23/06/2026      | <https://docs.aws.amazon.com/> |
| 5   | - **Thực hành Amazon ECS & CI/CD với AWS CodePipeline:** <br>&emsp; + Khởi tạo ECS Cluster chạy Fargate, cấu hình Task Definition lấy image từ ECR <br>&emsp; + Thiết lập AWS CodePipeline (kết nối CodeCommit/GitHub -> CodeBuild -> CodeDeploy) để tự động deploy phiên bản mới của container khi có thay đổi mã nguồn | 24/06/2026   | 24/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **AWS Storage Gateway:** <br>&emsp; + Tìm hiểu mô hình lưu trữ lai (Hybrid Storage) và các giải pháp giải quyết bài toán đồng bộ dữ liệu local lên Cloud <br>&emsp; + Nghiên cứu các loại Gateway: S3 File Gateway, Volume Gateway, Tape Gateway | 25/06/2026   | 25/06/2026      | <https://docs.aws.amazon.com/> |
| 7   | - **Thực hành AWS Storage Gateway:** <br>&emsp; + Tìm hiểu quy trình triển khai phần mềm Storage Gateway VM tại môi trường On-Premises ảo hóa <br>&emsp; + Mô phỏng liên kết S3 File Gateway với một Amazon S3 bucket để chia sẻ tệp tin qua giao thức mạng NFS/SMB | 26/06/2026   | 26/06/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 8:

* **Về Docker & Amazon ECR:**
  * Nắm vững quy trình đóng gói ứng dụng độc lập, giải quyết triệt để bài toán đồng bộ môi trường phát triển giữa Local và Production. 
  * Tạo thành công **Dockerfile** tối ưu hóa kích thước (sử dụng Multi-stage build), khởi tạo Private Repository trên **Amazon ECR**, phân quyền truy cập thông qua IAM và đẩy thành công Docker Image lên registry một cách an toàn.

* **Về Amazon ECS & AWS Fargate:**
  * Hiểu sâu sắc cách thức vận hành của mô hình Serverless Container. AWS Fargate giúp loại bỏ hoàn toàn gánh nặng quản lý, vá lỗi hệ điều hành và tự động co giãn (auto-scaling) tài nguyên máy chủ EC2 phía dưới.

  * Triển khai thành công ứng dụng web chạy trên **Amazon ECS** dưới dạng **AWS Fargate Tasks**. Thiết lập hệ thống chạy ổn định phía sau Application Load Balancer (ALB), cấu hình Health Check tự động phát hiện và thay thế các container bị lỗi.

* **Về AWS CodePipeline (CI/CD):**
  * Xây dựng thành công luồng CI/CD tự động hóa 100%. Mỗi khi có commit mới được đẩy lên kho mã nguồn, hệ thống tự động kích hoạt **AWS CodeBuild** để tạo Docker Image mới, tự động đẩy lên ECR và kích hoạt **AWS CodeDeploy** cập nhật phiên bản mới trên ECS Service theo cơ chế Rolling Update không gây gián đoạn dịch vụ (Zero Downtime).

* **Về AWS Storage Gateway:**
  * Phân biệt rõ ràng các kịch bản sử dụng thực tế của Storage Gateway. **S3 File Gateway** tối ưu cho việc chia sẻ file trực tiếp lên S3, **Volume Gateway** cung cấp block storage độ trễ thấp được sao lưu bằng EBS Snapshots, và **Tape Gateway** dùng để thay thế hệ thống băng từ vật lý lưu trữ truyền thống lâu năm.


  * Hiểu rõ cơ chế bộ nhớ đệm (Local Cache) của **S3 File Gateway** giúp các ứng dụng đặt tại On-Premises có thể truy xuất tệp tin với độ trễ nội bộ cực thấp, trong khi dữ liệu gốc vẫn được đồng bộ bất đồng bộ liên tục lên Amazon S3 bảo mật.