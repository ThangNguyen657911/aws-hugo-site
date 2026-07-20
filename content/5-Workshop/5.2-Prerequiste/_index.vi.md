---
title : "Khởi tạo Kho lưu trữ & Kênh thông báo (DynamoDB & SES)"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

#### Cấu hình cho DynamoDB cho ROMP
Tạo bảng DynamoDB ROMP-AlertHistory để lưu lịch sử cảnh báo từ module (Inventory, Expiry, Promotion, Sales), với cấu hình phù hợp .

![create stack](/images/5-Workshop/5.2-Prerequisite/DDB1.jpg)

* Ở ô tìm kiếm, gõ DynamoDB → chọn DynamoDB.
* Ở menu bên trái, chọn Tables.
* Bấm Create table.

![create stack](/images/5-Workshop/5.2-Prerequisite/DDB2.jpg)

* Table name: nhập chính xác ROMP-AlertHistory.
* Partition key: nhập AlertID, ở dropdown kiểu dữ liệu bên cạnh chọn String.
* Sort key: để trống, không tick chọn.

![create stack](/images/5-Workshop/5.2-Prerequisite/DDB3.jpg)

* Ở phần "Table settings", chọn Customize settings.
* Ở phần Table class: giữ mặc định DynamoDB Standard.

![create stack](/images/5-Workshop/5.2-Prerequisite/DDB4.jpg)

* Ở phần Capacity mode, chọn On-demand (không chọn Provisioned).

![create stack](/images/5-Workshop/5.2-Prerequisite/DDB5.jpg)

* Có thể thêm tag Project = ROMP để dễ quản lý chi phí/tài nguyên sau này. 
* Kéo xuống dưới cùng, review lại toàn bộ cấu hình.
* Bấm Create table.

![create stack](/images/5-Workshop/5.2-Prerequisite/DDB6.jpg)

* Đợi vài giây, status của bảng sẽ chuyển từ Creating → Active.

#### Cấu hình cho SES cho ROMP

Xác minh (verify) một địa chỉ email trong Amazon SES để Lambda có thể gửi cảnh báo (alert email) đến hộp thư của bạn.


![create stack](/images/5-Workshop/5.2-Prerequisite/SES1.jpg)

* Ở menu bên trái, chọn Identities (dưới mục Configuration).

* Bấm Create identity.

![create stack](/images/5-Workshop/5.2-Prerequisite/SES2.jpg)
* Ở "Identity type", chọn Email address.

* Ở ô "Email address", nhập địa chỉ email thật của bạn.



![create stack](/images/5-Workshop/5.2-Prerequisite/SES3.jpg)
* Kéo xuống dưới, phần Tags — có thể bỏ qua (optional) hoặc thêm tag Project: ROMP để dễ quản lý.

* Bấm Create identity.


![create stack](/images/5-Workshop/5.2-Prerequisite/SES4.jpg)

* AWS sẽ gửi ngay một email xác minh đến địa chỉ bạn vừa nhập, tiêu đề dạng "Amazon Web Services – Email Address Verification Request".

* Mở email đó, bấm vào link xác minh bên trong.



![create stack](/images/5-Workshop/5.2-Prerequisite/SES5.jpg)

* Trình duyệt sẽ mở ra trang xác nhận "Congratulations! You have successfully verified..." — đây là dấu hiệu thành công.

![create stack](/images/5-Workshop/5.2-Prerequisite/SES6.jpg)
Quay lại tab Identities trong SES Console, refresh trang.

* Trạng thái của email vừa tạo phải chuyển từ Pending verification → Verified. 

