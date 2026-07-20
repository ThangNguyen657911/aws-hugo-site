---
title : "Code Business Rule"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

#### Code Business Rule

Trong phần này sẽ trình bày Code Business Rule để đảm bảo nghiệp vụ của các dịch vụ.

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code1.jpg)

* Cấu trúc file trong dự án

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code2.jpg)

* Code file .env

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code3.jpg)

* Code file gitignore

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code4.jpg)

* Code requirement.txt

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code5.jpg)

* Code config.py

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code6.jpg)

* Code logger.py

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code7.jpg)

* Code oracle_server.py

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code8.jpg)



![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code9.jpg)



![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code10.jpg)

* Code repository/inventory.py

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code11.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code12.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code13.jpg)



![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code14.jpg)

* Code src/server/inventory_server.py

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code15.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code16.jpg)

* Code src/server/dynamodb_server.py

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code17.jpg)

* Code src/handler.py

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code18.jpg)

* Code src/lambda_function.py

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code19.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code20.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code21.jpg)



![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code22.jpg)

* Code src/server/ses_server.py


![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code25.jpg)

* Setup Dockerfile.lambda để chuẩn bị đóng gói code.

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code23.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code24.jpg)

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

