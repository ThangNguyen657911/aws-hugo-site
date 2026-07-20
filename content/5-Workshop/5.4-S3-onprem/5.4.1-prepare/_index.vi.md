---
title : "Cấu hình CloudWatch"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---



#### Triển khai CloudWatch



![route 53 diagram](/images/5-Workshop/5.4-S3-onprem/CW1.jpg)

* Kiểm tra region: đảm bảo vẫn đang ở ap-southeast-1 (Singapore).
* Ở ô tìm kiếm, gõ CloudWatch → chọn CloudWatch.
* Ở menu bên trái, chọn Log groups (dưới mục Logs).
* Bấm Create log group

![route 53 diagram](/images/5-Workshop/5.4-S3-onprem/CW2.jpg)

* Log group name: nhập chính xác /aws/lambda/romp-inventory.

* Retention setting: bấm vào dropdown, chọn 30 days.

![route 53 diagram](/images/5-Workshop/5.4-S3-onprem/CW3.jpg)

* Tags (tùy chọn): thêm Project = ROMP, Module = Inventory nếu muốn.
* Bấm Create.

![route 53 diagram](/images/5-Workshop/5.4-S3-onprem/CW4.jpg)

* Trạng thái sau khi cấu hình xong. 

