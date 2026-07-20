---
title : "Cấu hình Lambda"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.3.1 </b> "
---

#### Cấu hình Lambda

Trong phần này, tạo Lambda function trên AWS Console, gắn đúng IAM Role đã chuẩn bị cho 5.1, cấu hình runtime/memory/timeout phù hợp, và deploy code Inventory từ local lên AWS.

![overview](/images/5-Workshop/5.3-S3-vpc/Lambda1.jpg)

* Kiểm tra region: ap-southeast-1 (Singapore).
* Ở ô tìm kiếm, gõ Lambda → chọn Lambda.
* Bấm Create function.

![overview](/images/5-Workshop/5.3-S3-vpc/Lambda2.jpg)

* Chọn Author from scratch.

* Function name: nhập romp-inventory.

* Runtime: chọn dropdown → Python 3.12.

* Kéo xuống, bấm Create function.


![overview](/images/5-Workshop/5.3-S3-vpc/Lambda3.jpg)

* Click vào function vừa tạo.
* Chọn tab Configuration.
* Kéo xuống chọn Permissions
* Chọn Edit

![overview](/images/5-Workshop/5.3-S3-vpc/Lambda4.jpg)

* Memory: nhập 512 MB.

* Timeout: đổi sang 30 sec

* Ở dropdown Existing role, chọn ROMP-Lambda-ExecutionRole 

* Chọn Save 
![overview](/images/5-Workshop/5.3-S3-vpc/Lambda5.jpg)

* Chọn tab Code.

* Kéo xuống Runtime setting, chon edit.



![overview](/images/5-Workshop/5.3-S3-vpc/Lambda6.jpg)

* Nhập Handler theo file code của bạn. 

* Chọn Save. 




