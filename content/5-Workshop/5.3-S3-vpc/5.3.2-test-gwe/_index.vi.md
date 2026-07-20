---
title : "Code Business Rule"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

#### Code Business Rule

Trong phần này sẽ trình bày Code Business Rule để đảm bảo nghiệp vụ của các dịch vụ.

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code1.jpg)

* Cấu trúc file trong dự án

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code2.jpg)

* Code file .env

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code3.jpg)

* Code file gitignore

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code4.jpg)

* Code requirement.txt

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code5.jpg)

* Code config.py

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code6.jpg)

* Code logger.py

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code7.jpg)

* Code oracle_server.py

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code8.jpg)



![Create bucket](/images/5-Workshop/5.3-S3-vpc/code9.jpg)



![Create bucket](/images/5-Workshop/5.3-S3-vpc/code10.jpg)

* Code repository/inventory.py

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code11.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code12.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code13.jpg)



![Create bucket](/images/5-Workshop/5.3-S3-vpc/code14.jpg)

* Code src/server/inventory_server.py

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code15.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code16.jpg)

* Code src/server/dynamodb_server.py

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code17.jpg)

* Code src/handler.py

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code18.jpg)

* Code src/lambda_function.py

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code19.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code20.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code21.jpg)



![Create bucket](/images/5-Workshop/5.3-S3-vpc/code22.jpg)

* Code src/server/ses_server.py


![Create bucket](/images/5-Workshop/5.3-S3-vpc/code25.jpg)

* Setup Dockerfile.lambda để chuẩn bị đóng gói code.

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code23.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code24.jpg)

* Đóng gói code và các thư viện Python thành lambda_package.zip để upload lên AWS Lambda bằng Docker.

```
docker build `
-t romp-lambda `
-f Dockerfile.lambda `
..
docker rm -f romp-build 2>$null

docker create --name romp-build romp-lambda

docker cp romp-build:/build/python/lambda_package.zip lambda_package.zip

docker rm romp-build

```

