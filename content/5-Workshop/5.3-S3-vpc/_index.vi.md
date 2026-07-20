---
title : "Cấu hình Lambda và code Business Rule"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Cấu hình AWS Lambda và triển khai Business Rule
Sau khi hoàn thành các bước thiết lập hạ tầng như IAM Role, Amazon EventBridge, Amazon SES và Amazon DynamoDB, bước tiếp theo là xây dựng AWS Lambda để thực hiện việc giám sát dữ liệu từ hệ thống Oracle và xử lý các quy tắc nghiệp vụ (Business Rule).

AWS Lambda đóng vai trò là thành phần xử lý trung tâm của hệ thống ROMP. Lambda được Amazon EventBridge kích hoạt theo lịch định kỳ, sau đó kết nối đến cơ sở dữ liệu Oracle ở chế độ Read Only để lấy dữ liệu phục vụ giám sát. Dựa trên các quy tắc nghiệp vụ đã được định nghĩa, Lambda sẽ phân tích dữ liệu, xác định các trường hợp cần cảnh báo và thực hiện các hành động tương ứng như gửi email thông báo qua Amazon SES, lưu lịch sử cảnh báo vào Amazon DynamoDB và ghi log thực thi lên Amazon CloudWatch.



#### Triển khai Business Rule

Business Rule là thành phần quan trọng nhất của ROMP vì quyết định thời điểm hệ thống tạo cảnh báo. Thay vì chỉ lấy dữ liệu từ Oracle, Lambda sẽ đánh giá từng bản ghi theo các điều kiện nghiệp vụ đã được xác định trước.

Đối với module Inventory Monitoring, hệ thống kiểm tra số lượng tồn kho (quantity) của từng sản phẩm và so sánh với ngưỡng tồn kho an toàn (safety_stock). Quy tắc xử lý được xây dựng như sau:

Nếu quantity = 0, sản phẩm được xác định là Out of Stock và hệ thống tạo cảnh báo mức nghiêm trọng.
Nếu 0 < quantity ≤ safety_stock, sản phẩm được xác định là Low Stock và hệ thống tạo cảnh báo bổ sung hàng.
Nếu quantity > safety_stock, sản phẩm được xem là Normal, hệ thống chỉ ghi nhận kết quả mà không phát sinh cảnh báo.

Khi phát hiện một cảnh báo, Lambda sẽ thực hiện tuần tự các bước:

* Đọc dữ liệu từ Oracle Database.
* Đánh giá theo Business Rule.
* Tạo nội dung cảnh báo.
* Gửi email thông qua Amazon SES.
* Lưu lịch sử cảnh báo vào Amazon DynamoDB.
* Ghi log và các chỉ số thực thi lên Amazon CloudWatch.

Nhờ cơ chế xử lý tự động này, ROMP có thể giám sát liên tục tình trạng hàng tồn kho mà không cần sự can thiệp thủ công, giúp doanh nghiệp phát hiện sớm các rủi ro thiếu hàng và đưa ra quyết định bổ sung hàng hóa kịp thời.




####  [5.3.1 Cấu hình Lambda](5.3.1-create-gwe/)
####  [5.3.2 Code Business Rule](5.3.2-test-gwe/)


