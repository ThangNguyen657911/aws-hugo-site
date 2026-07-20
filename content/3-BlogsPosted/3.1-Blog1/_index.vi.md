---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# TỐI ƯU HÓA CHI PHÍ VÀ ĐỘ TIN CẬY BIG DATA: TRIỂN KHAI REMOTE SHUFFLE SERVICE TRÊN AMAZON EMR VỚI APACHE CELEBORN

Trong quá trình tối ưu hóa các hệ thống xử lý dữ liệu lớn (Big Data) chạy Apache Spark trên AWS, mình đã đúc kết được một giải pháp giải quyết triệt để bài toán đánh đổi giữa chi phí và độ tin cậy của hệ thống: **Sử dụng Apache Celeborn làm Remote Shuffle Service (RSS) trên Amazon EMR**.

## Những "nỗi đau" kinh điển khi xử lý Spark Shuffle lớn

Các tổ chức chạy các workload Apache Spark quy mô lớn thường xuyên đối mặt với các thách thức nghiêm trọng liên quan đến giai đoạn Shuffle (trao đổi dữ liệu giữa các stage), đặc biệt là khi muốn tối ưu chi phí bằng EC2 Spot Instances hoặc khi gặp dữ liệu bị lệch (data skew):

* **Gián đoạn do Spot Instance gây recomputation tốn kém:** Spot Instance giúp giảm tới 90% chi phí compute so với On-Demand nhưng có thể bị thu hồi chỉ với 2 phút báo trước. Khi một Spark executor trên Spot Instance bị thu hồi, dữ liệu shuffle cục bộ (local shuffle data) của nó sẽ mất sạch. Spark buộc phải tính toán lại (recompute) toàn bộ các stage thượng nguồn để tạo lại dữ liệu đó. Với các job xử lý hàng terabyte dữ liệu, việc này gây ra hiệu ứng domino làm chậm trễ runtime và làm "bốc hơi" số tiền tiết kiệm được từ Spot.
* **Lưu trữ shuffle cục bộ gây lãng phí tài nguyên (Over-provisioning):** Trong kiến trúc Hadoop truyền thống (bao gồm Amazon EMR trên EC2), External Shuffle Service (ESS) lưu trữ dữ liệu shuffle ngay trên ổ đĩa cục bộ của từng Node Manager. Điều này ép mọi node phải cấu hình dung lượng bộ nhớ và ổ đĩa rất lớn để dự phòng cho output shuffle, dù thực tế chỉ một vài node gánh vác phần lớn công việc. Đây chính là bài toán thắt nút cổ chai do ràng buộc chặt chẽ giữa Lưu trữ (Storage) và Tính toán (Compute).
* **Giữ chân Compute nhàn rỗi, không thể Scale-in:** Để tránh mất dữ liệu shuffle, logic scaling của Spark sẽ ngăn các node đang chứa dữ liệu shuffle thu hẹp quy mô (scale-down). Hậu quả là các EC2 node phải ngồi "chơi xơi nước" rất lâu sau khi task đã hoàn thành, đẩy chi phí lãng phí lên cao.

---

## Giải pháp cứu cánh: Apache Celeborn là gì?

![Blog1](/images/blog1.jpg)

**Apache Celeborn** là một dịch vụ Remote Shuffle Service (RSS) mã nguồn mở giúp tách biệt hoàn toàn (decouple) vòng đời của dữ liệu shuffle ra khỏi executor. Celeborn sử dụng kiến trúc Leader-Worker-Client:

* **Leader nodes:** Quản lý siêu dữ liệu (metadata).
* **Worker nodes:** Đọc và ghi các khối shuffle (shuffle blocks) độc lập.
* **Clients:** Tích hợp trực tiếp vào các engine tính toán (như Spark).

Thay vì ghi shuffle data xuống đĩa cục bộ của Spark executor, các executor sẽ đẩy (push) dữ liệu trực tiếp sang một cluster Celeborn dùng chung được tối ưu hóa cho lưu trữ.

> **Điểm cốt lõi:** Nhờ cơ chế này, các node executor của Amazon EMR có thể tự tin chạy 100% trên EC2 Spot Instances. Nếu Spot bị thu hồi, dữ liệu shuffle vẫn an toàn trên Celeborn cluster, các executor thoải mái scale-in/out tự do mà không sợ kích hoạt recomputation.

---

## Tổng quan kiến trúc giải pháp chuyên biệt

Trong giải pháp thực tế ở quy mô production, Celeborn được khuyến nghị chạy trên một cluster Amazon EKS tách biệt hoàn toàn với môi trường tính toán EMR (bao gồm cả EMR on EKS lẫn EMR on EC2).

Sự phân tách này mang lại lợi ích lớn vì hai workload này có profile tài nguyên hoàn toàn khác nhau: Celeborn chuyên sâu về I/O mạng và lưu trữ, trong khi Spark chuyên sâu về CPU và Memory. Từ đó, ta có thể lựa chọn các dòng EC2 instance tối ưu riêng cho từng cụm.

* **Kết nối Cross-cluster:** Cả cụm EMR và EKS chứa Celeborn nằm chung một Amazon VPC và chia sẻ các private subnets. AWS Load Balancer Controller trên EKS sẽ tạo một internal Network Load Balancer (NLB) trỏ đến các pod Celeborn. Các cụm EMR chỉ cần cấu hình endpoint `spark.celeborn.master.endpoints` về địa chỉ NLB này là có thể gọi dịch vụ thông qua cổng RPC 9097.
* **Đảm bảo an toàn dữ liệu (State Persistence):** Các nút Primary/Leader của Celeborn sử dụng cơ chế Raft consensus để quản lý trạng thái, được cấu hình dưới dạng StatefulSets kèm theo ổ đĩa Amazon EBS (gp3) để dữ liệu ghi log Raft sống sót qua các đợt restart pod. Trong khi đó, các Celeborn Worker sử dụng ổ đĩa local NVMe instance store để đạt tốc độ đọc/ghi shuffle cực cao. Để bù đắp tính chất ephemeral (tạm thời) của NVMe, hệ thống kích hoạt tính năng sao chép phân đoạn shuffle sang 2 worker khác nhau (`spark.celeborn.client.push.replicate.enabled=true`) để chống mất dữ liệu khi một worker gặp sự cố.
* **Hệ thống giám sát (Observability):** Sử dụng AWS Distro for OpenTelemetry (ADOT) collector triển khai trên EKS cluster để thu thập Prometheus metrics từ các pod Celeborn. Metrics sau đó được đẩy về các tùy chọn giám sát như Amazon Managed Service for Prometheus và trực quan hóa sinh động qua Amazon Grafana để theo dõi sức khỏe JVM, bộ nhớ đệm và hiệu năng shuffle theo thời gian thực.

---

## Các tham số cấu hình cốt lõi (Critical Configurations)

Để tích hợp mượt mà, bạn cần override một số cấu hình mặc định của Spark Client và Celeborn Server:

### 1. Cấu hình phía Spark Client (RSS Client)

Các tham số này được áp dụng khi submit job Spark qua EMR Steps API hoặc Spark Operator:

```properties
spark.shuffle.service.enabled = false
spark.shuffle.manager = org.apache.spark.shuffle.celeborn.SparkShuffleManager
spark.celeborn.client.spark.push.unsafeRow.fastWrite.enabled = false
spark.dynamicAllocation.shuffleTracking.enabled = false
```

* `spark.shuffle.service.enabled = false`: Tắt dịch vụ External Shuffle Service mặc định của Spark.
* `spark.shuffle.manager = org.apache.spark.shuffle.celeborn.SparkShuffleManager`: Kích hoạt Shuffle Manager của Celeborn thế chỗ.
* `spark.celeborn.client.spark.push.unsafeRow.fastWrite.enabled = false`: Tắt tối ưu hóa UnsafeRow của Celeborn nhằm đảm bảo tương thích hoàn hảo với Spark runtime đã tối ưu của Amazon EMR.
* `spark.dynamicAllocation.shuffleTracking.enabled = false`: Vô hiệu hóa tính năng shuffle tracking của Spark để nhường quyền quản lý hoàn toàn cho Celeborn.

### 2. Cấu hình phía Celeborn Server (RSS Server)

Được thiết lập thông qua tệp Helm `values.yaml` khi deploy lên EKS:

```yaml
master.replicas = 3
worker.volumes = 4 × hostPath (/mnt/nvme/disk1-4)
```

* `master.replicas = 3`: Số lượng node leader tối thiểu để duy trì Raft quorum phòng vệ lỗi.
* `worker.volumes = 4 × hostPath (/mnt/nvme/disk1-4)`: Mount trực tiếp ổ đĩa NVMe cục bộ để đạt băng thông I/O tối đa.

---

## Kết luận

Mô hình Remote Shuffle Service với Apache Celeborn trên Amazon EMR chứng minh rằng kiến trúc tách rời lưu trữ và tính toán (Decoupled Storage-Compute) không chỉ áp dụng cho tầng Data Lake (S3) mà còn tối ưu vượt trội cho cả tầng dữ liệu tạm thời (Shuffle Data).

Giải pháp này đập tan nỗi sợ Spot Instance bị gián đoạn, tối ưu hóa kích thước cluster và cởi trói hoàn toàn cho khả năng Auto-scaling của Spark. Giờ đây, bạn không còn phải chọn giữa một hạ tầng giá rẻ hay một hệ thống chạy ổn định nữa – Celeborn mang lại cho bạn cả hai trên Amazon EMR.

Tham khảo nguồn tại: [aws.amazon.com/vi/blogs/big-data/high-performance-remote-shuffle-service-on-amazon-emr-with-apache-celeborn](https://aws.amazon.com/vi/blogs/big-data/high-performance-remote-shuffle-service-on-amazon-emr-with-apache-celeborn/).

Mọi người có ai đang gặp ác mộng về chi phí Shuffle data hay lỗi Spot instance không, cùng thảo luận ở phía dưới nhé!