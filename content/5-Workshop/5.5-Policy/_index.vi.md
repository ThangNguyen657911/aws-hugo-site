---
title : "Kết quả đạt được"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---

### Sau khi thực hiện xong kiểm tra kết quả 

#### Kiểm tra Lambda

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ1.jpg)

* Ở ô tìm kiếm chọn Lambda.
* Chọn function nằm bên trái.
* Chon function romp-inventory.


![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ2.jpg)

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ3.jpg)

* Chọn tab code.
* Chọn update.
* Chọn Choose file.
* Lúc này bạn sẽ update file đã đóng gói thực hiện ở mục [5.3.2](5.3.2-test-gwe/)
* Chọn update.

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ4.jpg)

* Chọn test.
* Kết quả đạt được ở output lambda.


#### Kiểm tra EventBridge và SES
![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ5.jpg)

* Sau đó bạn mở email đã cài đặt để nhận thông báo
* Kết quả đạt được **EventBridge** cứ mỗi 5 phút sẽ tự động kiểm tra database và cập nhật cảnh báo cho các sản phẩm đã hết hoặc sắp hết.
* Kết quả đạt được của SES gửi được mail khi Business Rule trong Lambda gửi cảnh báo.
* Thời gian gửi mail tùy chọn.

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ6.jpg)


![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ7.jpg)

* Nội dung mail được cảnh báo.

#### Kiểm tra DynamoDB

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ11.jpg)

* Tại ô tìm kiếm gõ DynamoDB.
* Chọn mục table.
* Chọn ROMP-AlertHistory

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ12.jpg)

* Chọn Explore table items 

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ8.jpg)

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ9.jpg)

* Kết quả được lưu vào DynamoDB

#### Kiểm tra CloudWatch

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ13.jpg)

* Ở ô tìm kiếm gõ CloudWatch.
* Chọn mục LogManagement.
* Chọn /aws/lambda/romp-inventory.

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ14.jpg)

* Chọn log mới nhất.

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ10.jpg)

* Kết quả ghi nhận ở CloudWatch.

