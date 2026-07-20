---
title : "Code Business Rule"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

#### Code Business Rule

In this section, we will present the Code Business Rule to ensure the business logic of the services.

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code1.jpg)

* Project directory structure

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code2.jpg)

* Code for `.env` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code3.jpg)

* Code for `.gitignore` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code4.jpg)

* Code for `requirements.txt` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code5.jpg)

* Code for `config.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code6.jpg)

* Code for `logger.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code7.jpg)

* Code for `oracle_server.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code8.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code9.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code10.jpg)

* Code for `repository/inventory.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code11.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code12.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code13.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code14.jpg)

* Code for `src/server/inventory_server.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code15.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code16.jpg)

* Code for `src/server/dynamodb_server.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code17.jpg)

* Code for `src/handler.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code18.jpg)

* Code for `src/lambda_function.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code19.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code20.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code21.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code22.jpg)

* Code for `src/server/ses_server.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code25.jpg)

* Set up `Dockerfile.lambda` to prepare for code packaging.

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code23.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/code24.jpg)

* Package the code and Python libraries into `lambda_package.zip` to upload to AWS Lambda using Docker.

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