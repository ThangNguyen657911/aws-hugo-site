---
title: "Bản đề xuất"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

Tại phần này, tôi trình bày tổng quan về workshop dự kiến thực hiện trong chương trình thực tập. Nội dung bao gồm mục tiêu của hệ thống, kiến trúc giải pháp, công nghệ AWS được sử dụng, lộ trình triển khai, chi phí dự kiến, đánh giá rủi ro và kết quả mong muốn sau khi hoàn thành.

# Retail Operations Monitoring Platform (ROMP)

## Giải pháp giám sát hoạt động bán lẻ theo thời gian thực trên nền tảng AWS Serverless

---

# 1. Tóm tắt điều hành

Retail Operations Monitoring Platform (ROMP) là một hệ thống giám sát hoạt động bán lẻ được xây dựng theo kiến trúc **AWS Serverless** nhằm tự động theo dõi dữ liệu từ hệ thống quản lý hiện có và phát hiện các vấn đề quan trọng trong quá trình vận hành cửa hàng.

Thay vì thay thế hệ thống ERP hoặc POS đang sử dụng, ROMP đóng vai trò như một **Monitoring Platform**, kết nối tới cơ sở dữ liệu Oracle ở chế độ **Read Only**, định kỳ phân tích dữ liệu bằng các Business Rule và gửi cảnh báo ngay khi phát hiện bất thường.

Các cảnh báo được gửi qua Amazon SES, đồng thời toàn bộ lịch sử cảnh báo được lưu vào Amazon DynamoDB để phục vụ việc truy xuất và thống kê sau này.

Hệ thống được thiết kế hoàn toàn theo mô hình **Event-Driven Architecture**, sử dụng các dịch vụ Serverless của AWS giúp giảm chi phí vận hành, dễ mở rộng và gần như không phải quản lý hạ tầng máy chủ.

Mục tiêu chính của dự án là xây dựng một nền tảng giám sát có khả năng:

- Theo dõi tồn kho theo thời gian thực.
- Phát hiện hàng sắp hết.
- Phát hiện hàng hết hạn.
- Theo dõi chương trình khuyến mãi.
- Theo dõi doanh số bán hàng.
- Gửi cảnh báo tự động.
- Lưu lịch sử cảnh báo.
- Theo dõi log và metric của toàn bộ hệ thống.

---

# 2. Tuyên bố vấn đề

## Vấn đề hiện tại

Trong nhiều doanh nghiệp bán lẻ, hệ thống ERP hoặc POS chỉ tập trung phục vụ các nghiệp vụ như bán hàng, nhập kho hoặc quản lý sản phẩm. Tuy nhiên các hệ thống này thường không có cơ chế giám sát chủ động.

Ví dụ:

- Không tự động phát hiện sản phẩm sắp hết hàng.
- Không cảnh báo khi sản phẩm đã hết hàng.
- Không phát hiện sản phẩm sắp hết hạn sử dụng.
- Không nhắc nhở khi chương trình khuyến mãi chuẩn bị kết thúc.
- Không phát hiện doanh số bất thường.
- Người quản lý phải kiểm tra dữ liệu thủ công.

Khi số lượng cửa hàng và dữ liệu tăng lên, việc theo dõi bằng tay sẽ tiêu tốn rất nhiều thời gian và dễ xảy ra sai sót.

Ngoài ra, việc chỉnh sửa trực tiếp vào hệ thống nghiệp vụ có thể gây ảnh hưởng tới hoạt động kinh doanh.

Do đó cần một nền tảng giám sát độc lập, chỉ đọc dữ liệu từ hệ thống hiện có nhưng vẫn có khả năng phân tích và đưa ra cảnh báo theo thời gian thực.

---

## Giải pháp

Retail Operations Monitoring Platform được xây dựng như một lớp giám sát độc lập.

Hệ thống sử dụng Amazon EventBridge để kích hoạt AWS Lambda theo lịch định kỳ. Lambda sẽ kết nối tới Oracle Database bằng tài khoản chỉ có quyền **Read Only**, đọc dữ liệu cần thiết và áp dụng các Business Rule để xác định trạng thái của từng nghiệp vụ.

Nếu phát hiện bất thường, Lambda sẽ:

- gửi email thông qua Amazon SES;
- lưu lịch sử cảnh báo vào DynamoDB;
- ghi log lên Amazon CloudWatch.

Việc xử lý hoàn toàn tự động giúp người quản trị nhận được thông tin ngay khi có sự cố mà không cần kiểm tra thủ công.

---

## Lợi ích và ROI

Việc triển khai ROMP mang lại nhiều lợi ích:

- Giảm đáng kể thời gian kiểm tra dữ liệu thủ công.
- Phát hiện sớm các vấn đề trong vận hành.
- Giảm nguy cơ mất doanh thu do hết hàng.
- Giảm thất thoát do sản phẩm hết hạn.
- Chủ động quản lý chương trình khuyến mãi.
- Có lịch sử cảnh báo phục vụ kiểm toán.
- Có log đầy đủ để phân tích sự cố.

Do sử dụng hoàn toàn các dịch vụ Serverless nên chi phí vận hành thấp và phù hợp với doanh nghiệp vừa và nhỏ.

---

# 3. Kiến trúc giải pháp

ROMP được xây dựng theo kiến trúc Event-Driven kết hợp Serverless trên AWS.

Luồng hoạt động tổng quát như sau:

1. Amazon EventBridge kích hoạt Lambda theo lịch.
2. Lambda kết nối Oracle Database.
3. Oracle chỉ cung cấp dữ liệu ở chế độ Read Only.
4. Lambda áp dụng Business Rules.
5. Nếu phát hiện cảnh báo:
   - gửi Email bằng Amazon SES;
   - lưu lịch sử vào DynamoDB.
6. CloudWatch thu thập toàn bộ Log và Metrics.

Kiến trúc này giúp các thành phần hoạt động độc lập, dễ mở rộng và giảm tối đa chi phí vận hành.

![ROMP Architecture](/images/2-Proposal/romp.jpg)

---

## Dịch vụ AWS sử dụng

**Amazon EventBridge**

Điều phối việc chạy các Lambda theo lịch định kỳ.

**AWS Lambda**

Thực hiện toàn bộ Business Logic của hệ thống.

Các Lambda được chia thành các module:

- Inventory Monitoring
- Expiry Monitoring
- Promotion Monitoring
- Sales Monitoring

**Amazon SES**

Gửi email cảnh báo tới quản trị viên.

**Amazon DynamoDB**

Lưu lịch sử các cảnh báo đã được tạo.

**Amazon CloudWatch**

Theo dõi Log, Metric và hỗ trợ giám sát hệ thống.

**AWS IAM**

Quản lý quyền truy cập theo nguyên tắc Least Privilege.

**Oracle Database**

Nguồn dữ liệu chính của doanh nghiệp.

Lambda chỉ có quyền SELECT.

---

## Thiết kế thành phần

Hệ thống được chia thành nhiều module độc lập.

### Inventory Monitoring

Theo dõi số lượng tồn kho.

Business Rule:

- Quantity = 0 → Out Of Stock
- Quantity ≤ Safety Stock → Low Stock

### Expiry Monitoring

Kiểm tra ngày hết hạn sản phẩm.

Business Rule:

- Hết hạn.
- Sắp hết hạn.

### Promotion Monitoring

Kiểm tra trạng thái chương trình khuyến mãi.

Business Rule:

- Sắp kết thúc.
- Đã hết hiệu lực.

### Sales Monitoring

Theo dõi doanh số.

Business Rule:

- Doanh số giảm mạnh.
- Doanh số vượt ngưỡng.

Mỗi module được triển khai bằng một Lambda độc lập giúp dễ bảo trì và mở rộng.

---

# 4. Triển khai kỹ thuật

Quá trình phát triển hệ thống được chia thành nhiều giai đoạn.

## Giai đoạn 1

Khảo sát yêu cầu và thiết kế kiến trúc.

Bao gồm:

- nghiên cứu AWS Well-Architected Framework;
- lựa chọn kiến trúc Serverless;
- xác định Business Rule.

---

## Giai đoạn 2

Thiết lập môi trường AWS.

Bao gồm:

- IAM Role;
- SES;
- DynamoDB;
- CloudWatch;
- EventBridge;
- Lambda.

---

## Giai đoạn 3

Kết nối Oracle Database.

Bao gồm:

- xây dựng Oracle Service;
- kiểm tra kết nối;
- truy vấn dữ liệu Read Only.

---

## Giai đoạn 4

Phát triển Business Rule.

Mỗi Lambda sẽ xử lý một nhóm nghiệp vụ riêng.

---

## Giai đoạn 5

Kiểm thử toàn bộ hệ thống.

Bao gồm:

- Unit Test.
- Integration Test.
- End-to-End Test.

---


# 5. Ước tính ngân sách

Do dự án sử dụng các dịch vụ Serverless nên chi phí phát sinh chủ yếu đến từ số lượng request và dung lượng lưu trữ.

Ước tính khi triển khai trong AWS Free Tier:

| Dịch vụ | Chi phí |
|----------|---------|
| AWS Lambda | Gần như miễn phí |
| Amazon DynamoDB | Free Tier |
| Amazon SES | Chi phí rất thấp |
| Amazon EventBridge | Free Tier |
| Amazon CloudWatch | Free Tier |
| IAM | Miễn phí |

Tổng chi phí ước tính chỉ vài USD mỗi tháng nếu vượt khỏi Free Tier.

---

# 6. Đánh giá rủi ro

## Ma trận rủi ro

| Rủi ro | Mức ảnh hưởng | Khả năng |
|---------|---------------|-----------|
| Oracle không kết nối | Cao | Trung bình |
| SES chưa Verify Email | Trung bình | Trung bình |
| Sai Business Rule | Cao | Thấp |
| Vượt Free Tier | Trung bình | Thấp |
| Lỗi Lambda | Cao | Trung bình |

---

## Chiến lược giảm thiểu

- Chỉ sử dụng quyền Read Only.
- Kiểm thử từng Lambda độc lập.
- Theo dõi CloudWatch Logs.
- Thiết lập Budget Alert.
- Áp dụng IAM Least Privilege.

---

## Kế hoạch dự phòng

Nếu Lambda gặp lỗi:

- EventBridge sẽ kích hoạt lại ở chu kỳ tiếp theo.
- CloudWatch lưu đầy đủ log để phân tích.
- Có thể triển khai lại Lambda mà không ảnh hưởng hệ thống Oracle.

---

# 7. Kết quả kỳ vọng

Sau khi hoàn thành workshop, hệ thống sẽ đáp ứng các mục tiêu sau:

- Xây dựng thành công nền tảng giám sát bán lẻ trên AWS Serverless.
- Tự động phát hiện các sự kiện bất thường trong dữ liệu Oracle.
- Gửi email cảnh báo theo thời gian thực.
- Lưu trữ lịch sử cảnh báo trong DynamoDB.
- Theo dõi hoạt động của hệ thống bằng CloudWatch.
- Áp dụng kiến trúc Event-Driven theo AWS Well-Architected Framework.
- Có khả năng mở rộng thêm nhiều Business Module trong tương lai mà không cần thay đổi kiến trúc tổng thể.

Thông qua dự án này, người thực hiện không chỉ nắm được cách sử dụng các dịch vụ AWS Serverless mà còn hiểu được cách thiết kế một hệ thống giám sát thực tế theo tiêu chuẩn doanh nghiệp, từ đó làm nền tảng cho các dự án Cloud Native quy mô lớn hơn trong tương lai.