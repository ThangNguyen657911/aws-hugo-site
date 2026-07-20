---
title : "Cấu hình EventBridge"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.4.2 </b> "
---

#### Triển khai EventBridge

![name](/images/5-Workshop/5.4-S3-onprem/EB1.jpg)

* Kiểm tra region: ap-southeast-1 (Singapore).
* Ở ô tìm kiếm, gõ EventBridge → chọn Amazon EventBridge.
* Ở menu bên trái, chọn Rules.
* Bấm Create rule.

![name](/images/5-Workshop/5.4-S3-onprem/EB2.jpg)

* Name: nhập chính xác ROMP-Inventory-Schedule.

* Description: Triggers romp-inventory Lambda every 5 minutes during development phase.

* Time bạn có thể tùy chọn

* Bấm Next.

![name](/images/5-Workshop/5.4-S3-onprem/EB3.jpg)

* Schedule pattern: chọn A schedule that runs at a regular rate.

* Rate expression: nhập giá trị 5, đơn vị chọn Minutes.

* Console sẽ tự hiển thị preview dạng rate(5 minutes) — xác nhận đúng.

* Thời gian bạn có thể tùy chọn.

* Bấm Next.

![name](/images/5-Workshop/5.4-S3-onprem/EB4.jpg)

* Target type: chọn AWS service.

* Select a target: ở dropdown, gõ/chọn Lambda function.

* Function: ở dropdown chọn function, gõ romp-inventory để lọc, chọn đúng function đã deploy

* Bấm Next.

![name](/images/5-Workshop/5.4-S3-onprem/EB5.jpg)

* Thêm tag Project = ROMP, Module = Inventory.

* Bấm Next.

![name](/images/5-Workshop/5.4-S3-onprem/EB6.jpg)

* Kiểm tra lại toàn bộ:
* Name: ROMP-Inventory-Schedule
* Schedule: rate(5 minutes)
* Target: Lambda romp-inventory

* Bấm Create rule.

![name](/images/5-Workshop/5.4-S3-onprem/EB7.jpg)

* Trạng thái sau khi cấu hình xong. 


