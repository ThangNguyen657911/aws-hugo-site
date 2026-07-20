---
title: "Quyền IAM & Thiết lập nền tảng "
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

### Giới thiệu về VPC Endpoint trong hệ thống ROMP

Điểm cuối VPC (VPC Endpoint) là một thiết bị ảo được cô lập về mặt logic, có khả năng mở rộng theo chiều ngang, tính dự phòng và độ sẵn sàng cao. Nó cho phép giao tiếp liền mạch giữa các tài nguyên điện toán (workloads) của bạn và các dịch vụ AWS được hỗ trợ mà không gây ra rủi ro về tính sẵn sàng hoặc làm lộ lưu lượng truy cập ra ngoài mạng Internet công cộng.

Trong kiến trúc của **Retail Operations Monitoring Platform (ROMP)**, việc bảo vệ dữ liệu trong quá trình truyền tải là vô cùng nghiêm ngặt:
* **Gateway Endpoint:** Được sử dụng bởi các hàm AWS Lambda trong mạng nội bộ VPC để đọc/ghi dữ liệu an toàn trực tiếp vào Amazon DynamoDB bằng cách sử dụng các địa chỉ IP Private.
* **Interface Endpoint (AWS PrivateLink):** Được sử dụng để thiết lập các kết nối riêng tư đến các dịch vụ AWS khác (như Amazon SES hoặc Amazon CloudWatch) hoặc làm cầu nối kết nối an toàn giữa lớp giám sát trên đám mây và hạ tầng trung tâm dữ liệu của doanh nghiệp.

---

### Tổng quan về môi trường Workshop

Để mô phỏng một môi trường doanh nghiệp thực tế, workshop này sử dụng một mô hình mạng Hybrid kết hợp nhiều VPC bao gồm hai môi trường chính:
1. **"ROMP Cloud VPC":** Môi trường này lưu trữ các thành phần giám sát Serverless của bạn, bao gồm các hàm AWS Lambda (Inventory, Expiry, Promotion, và Sales Monitoring) được cấu hình bên trong các Private Subnets, cùng với các IAM Roles được thiết kế riêng để các dịch vụ tương tác an toàn.
2. **"On-Premises Network VPC":** Môi trường này mô phỏng mạng trung tâm dữ liệu truyền thống hoặc mạng nhà máy của công ty, nơi đặt cơ sở dữ liệu cốt lõi **Oracle Database**.


---

### Phần triển khai: 

#### Quyền IAM

![overview](/images/5-Workshop/5.1-Workshop-overview/IAM1.jpg)

* Ở ô tìm kiếm trên cùng, gõ IAM → chọn IAM.
* Ở menu bên trái, chọn Roles.
* Bấm Create role.

![overview](/images/5-Workshop/5.1-Workshop-overview/IAM2.jpg)

* Ở màn "Select trusted entity type", chọn AWS service.
* Ở phần "Use case", trong dropdown chọn Lambda.
* Bấm Next.

![overview](/images/5-Workshop/5.1-Workshop-overview/IAM3.jpg)


* Ở ô tìm kiếm permission policies, gõ AWSLambdaBasicExecutionRole → tick chọn.



![overview](/images/5-Workshop/5.1-Workshop-overview/IAM4.jpg)

* Gõ tiếp AWSLambdaVPCAccessExecutionRole → tick chọn. 

* Bấm Next.



![overview](/images/5-Workshop/5.1-Workshop-overview/IAM5.jpg)

* Role name: gõ chính xác ROMP-Lambda-ExecutionRole.

* Description : Shared execution role for ROMP Lambda functions (Inventory, Expiry, Promotion, Sales).

* Kéo xuống dưới, review lại Trusted entities và Permissions.

* Bấm Create role.


![overview](/images/5-Workshop/5.1-Workshop-overview/IAM6.jpg)

* Sau khi tạo xong, bạn sẽ ở trang Role vừa tạo (hoặc vào Roles → ROMP-Lambda-ExecutionRole).

* Tab Permissions → bấm Add permissions → Create inline policy.





![overview](/images/5-Workshop/5.1-Workshop-overview/IAM7.jpg)

Chọn tab JSON, dán policy sau:

```properties
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ROMPDynamoDBAccess",
      "Effect": "Allow",
      "Action": [
        "dynamodb:PutItem",
        "dynamodb:GetItem",
        "dynamodb:UpdateItem",
        "dynamodb:Query"
      ],
      "Resource": "arn:aws:dynamodb:AP_SOUTHEAST_1:ACCOUNT_ID:table/ROMP-AlertHistory"
    }
  ]
}
```


![overview](/images/5-Workshop/5.1-Workshop-overview/IAM8.jpg)

* Bấm Next.
* Policy name: gõ ROMP-DynamoDB.
* Bấm Create policy.

![overview](/images/5-Workshop/5.1-Workshop-overview/IAM9.jpg)

Add permissions → Create inline policy → JSON, dán:

```properties
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ROMPSESSendEmail",
      "Effect": "Allow",
      "Action": [
        "ses:SendEmail",
        "ses:SendRawEmail"
      ],
      "Resource": "*"
    }
  ]
}
```



![overview](/images/5-Workshop/5.1-Workshop-overview/IAM10.jpg)

Policy name: ROMP-SES.
Bấm Create policy.

#### VPC
![overview](/images/5-Workshop/5.1-Workshop-overview/VPC1.jpg)
* Truy cập vào VPC Dashboard trên AWS Console.

* Chọn Create VPC.

![overview](/images/5-Workshop/5.1-Workshop-overview/VPC2.jpg)
* Tại mục Resources to create, chọn VPC and more.


![overview](/images/5-Workshop/5.1-Workshop-overview/VPC3.jpg)
* Name tag auto-generation: Nhập ROMP-VPC.

* IPv4 CIDR block: 10.0.0.0/16.

![overview](/images/5-Workshop/5.1-Workshop-overview/VPC4.jpg)
Number of Availability Zones (AZs): Chọn 1 (Để tiết kiệm chi phí và đúng thiết kế của bạn. Chọn AZ bất kỳ, ví dụ: ap-southeast-1a).

* Number of Public subnets: Chọn 1.

* Sửa CIDR block của Public Subnet thành: 10.0.1.0/24.

* Number of Private subnets: Chọn 1.

* Sửa CIDR block của Private Subnet thành: 10.0.2.0/24.

![overview](/images/5-Workshop/5.1-Workshop-overview/VPC5.jpg)
* NAT Gateways: Chọn 1 per AZ (AWS sẽ tự động tạo 1 NAT Gateway và đặt nó vào Public Subnet của bạn).

* VPC Endpoints: Chọn None (Nếu không cần thiết, để tránh phát sinh chi phí).

* Nhấn **Create VPC** và đợi vài phút để AWS tạo toàn bộ hạ tầng mạng.

#### Tạo Security Group cho Lambda

Vì EC2 cần biết chính xác Security Group nào của Lambda được phép gọi vào, bạn cần khởi tạo nhóm bảo mật cho Lambda trước.

![overview](/images/5-Workshop/5.1-Workshop-overview/SG1.jpg)

* Truy cập EC2 Dashboard trên AWS Console.

* Ở menu bên trái, chọn Security Groups > Nhấn Create security group.

![overview](/images/5-Workshop/5.1-Workshop-overview/SG2.jpg)

* Cấu hình thông số:

* Security group name: Nhập ROMP-Lambda-SG (hoặc tên tùy ý bạn).

* Description: Nhập mô tả (ví dụ: SG cho Lambda function).

* VPC: Chọn đúng VPC của bạn (ROMP-VPC-vpc / vpc-0ef1b3e18f4d1d7fb).

![overview](/images/5-Workshop/5.1-Workshop-overview/SG3.jpg)

* Nhấn Create security group.

* Sau khi tạo xong, hãy Copy lại mã Security Group ID vừa tạo


#### Tạo Security Group cho EC2 Oracle

![overview](/images/5-Workshop/5.1-Workshop-overview/SG1.jpg)

* Tiếp tục nhấn nút Create security group

![overview](/images/5-Workshop/5.1-Workshop-overview/SG4.jpg)

* Cấu hình thông số cơ bản:

* Security group name: Nhập chính xác ROMP-Oracle-SG.

* Description: Nhập mô tả (ví dụ: SG cho EC2 Oracle Database).

* VPC: Chọn đúng VPC của bạn (ROMP-VPC-vpc / vpc-0ef1b3e18f4d1d7fb).

![overview](/images/5-Workshop/5.1-Workshop-overview/SG5.jpg)

**Tại mục Inbound rules (Quy tắc đi vào), nhấn Add rule để thêm 2 dòng sau:**

**Dòng 1: Cấp quyền cho Lambda gọi vào Oracle DB**
* Type: Chọn Custom TCP.

* Port range: Nhập 1521 (Cổng mặc định của Oracle).

* Source: Tích vào ô bên cạnh, chọn Custom. Sau đó, bạn gõ hoặc paste cái mã sg-... của ROMP-Lambda-SG (đã làm ở Bước 1) vào ô này.

**Dòng 2: Cấp quyền SSH cho máy tính của bạn**
* Type: Chọn SSH.

* Port range: Mặc định sẽ là 22.

* Source: Bấm vào menu thả xuống và chọn My IP.

* Nhấn Create security group.


![overview](/images/5-Workshop/5.1-Workshop-overview/SG6.jpg)

* Giao diện sau khi cấu hình xong

**Gắn các Security Group này vào EC2 và Lambda**

Sau khi đã tạo xong 2 nhóm bảo mật, bạn chỉ cần gán chúng vào các tài nguyên tương ứng:

Đối với Lambda: Vào cấu hình Lambda của bạn > Tab Configuration > VPC > Nhấn Edit và chọn nhóm ROMP-Lambda-SG.

Đối với EC2 Oracle: Vào danh sách EC2 > Tích chọn EC2 Oracle > Bấm Actions > Security > Change security groups > Chọn nhóm ROMP-Oracle-SG (và gỡ các SG mặc định khác ra nếu có).

#### Khởi tạo EC2 Instance

![overview](/images/5-Workshop/5.1-Workshop-overview/EC21.jpg)
* Truy cập EC2 Dashboard > Nhấn Launch instance.

![overview](/images/5-Workshop/5.1-Workshop-overview/EC22.jpg)
* Name and tags: Nhập tên ROMP-Oracle-Server

* Application and OS Images (Amazon Machine Image):

* Chọn Ubuntu.



![overview](/images/5-Workshop/5.1-Workshop-overview/EC23.jpg)

* Phần Amazon Machine Image (AMI): Chọn bản Ubuntu Server 24.04 LTS hoặc 22.04 LTS (đều được hỗ trợ Free Tier).

* Instance type: Chọn t3.small 

![overview](/images/5-Workshop/5.1-Workshop-overview/EC24.jpg)

* Network settings: Nhấn Edit ở góc phải:

* VPC: Chọn đúng ROMP-VPC-vpc.

* Subnet: Chọn đúng Private Subnet (10.0.2.0/24).

* Auto-assign public IP: Chọn Disable.

* Firewall (security groups): Tích vào Select existing security group và chọn đúng nhóm ROMP-Oracle-SG mà bạn đã tạo ở bước trước.

* Nhấn Launch instance và đợi server khởi tạo xong.

#### SSH vào EC2

* Sau khi tạo EC2 bạn download file .pem và tạo folder keys cho file .pem

* Sau đó bạn copy IP và gõ lệnh ssh -i .\ROMP-Oracle-Key.pem ubuntu@<IP>
* Kết quả như hình sau: 
![overview](/images/5-Workshop/5.1-Workshop-overview/SSH1.jpg)

**Cập nhật Ubuntu và cài các thư viện bổ trợ**

1. Cập nhật danh sách gói phần mềm


* sudo apt-get update && sudo apt-get upgrade -y

2. Cài đặt các thư viện hệ thống mà Oracle yêu cầu
* sudo apt-get install -y alien libaio1 unixodbc dnsutils network-manager

3. Tạo một thư mục tạm để chuẩn bị tải file cài đặt
* mkdir ~/oracle21c && cd ~/oracle21c

![overview](/images/5-Workshop/5.1-Workshop-overview/SSH2.jpg)
![overview](/images/5-Workshop/5.1-Workshop-overview/SSH3.jpg)

4. Tải file RPM của Oracle XE 21c (nặng khoảng hơn 2GB)
* wget https://download.oracle.com/otn-pub/otn_software/db-express/oracle-database-xe-21c-1.0-1.x86_64.rpm

5. Chuyển đổi RPM sang gói DEB của Ubuntu
(Lưu ý quan trọng: Lệnh này xử lý gói rất nặng, có thể mất từ 10 - 15 phút. Khi chạy màn hình sẽ bất động một lúc, bạn cứ kiên nhẫn đợi cho đến khi nó chạy xong nhé)
* sudo alien --to-deb --scripts oracle-database-xe-21c-1.0-1.x86_64.rpm

6. Tiến hành cài đặt file .deb vừa được tạo ra vào hệ thống
* sudo dpkg -i oracle-database-xe-21c_*.deb

7. Chạy lệnh cấu hình khởi tạo Database
* sudo /etc/init.d/oracle-xe-21c configure

Khởi động dịch vụ Oracle
* sudo systemctl start oracle-xe-21c

Cho phép Oracle tự động bật mỗi khi EC2 khởi động lại
* sudo systemctl enable oracle-xe-21c

Kiểm tra trạng thái xem có chữ màu xanh "active (running)" hay chưa
* sudo systemctl status oracle-xe-21c

**Bước Oracle Deployment**
```properties
Bước 1. Tải Oracle XE Image
docker pull gvenzl/oracle-xe:21-slim

Bước 2. Kiểm tra image
docker images

Bước 3. Tạo thư mục lưu dữ liệu

mkdir -p ~/oracle-data

Bước 4. Chạy Oracle XE

docker run -d \
--name oracle-xe \
-p 1521:1521 \
-p 5500:5500 \
-e ORACLE_PASSWORD=123456 \
-v ~/oracle-data:/opt/oracle/oradata \
gvenzl/oracle-xe:21-slim

Bước 5. Kiểm tra container

docker ps

Bước 6. Theo dõi log

docker logs -f oracle-xe

```

* Sau bước này Oracle đã sẵn sàng lên EC2

