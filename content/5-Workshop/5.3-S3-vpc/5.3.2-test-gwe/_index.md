---
title : "Code Business Rule"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

#### Code Business Rule

In this section, we will present the Code Business Rule to ensure the business logic of the services.

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code1.jpg)

* Project directory structure

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code2.jpg)

* Code for `.env` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code3.jpg)

* Code for `.gitignore` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code4.jpg)

* Code for `requirements.txt` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code5.jpg)

* Code for `config.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code6.jpg)

* Code for `logger.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code7.jpg)

* Code for `oracle_server.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code8.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code9.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code10.jpg)

* Code for `repository/inventory.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code11.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code12.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code13.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code14.jpg)

* Code for `src/server/inventory_server.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code15.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code16.jpg)

* Code for `src/server/dynamodb_server.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code17.jpg)

* Code for `src/handler.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code18.jpg)

* Code for `src/lambda_function.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code19.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code20.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code21.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code22.jpg)

* Code for `src/server/ses_server.py` file

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code25.jpg)

* Set up `Dockerfile.lambda` to prepare for code packaging.

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code23.jpg)

![Create bucket](/images/5-Workshop/5.3-S3-vpc/Code24.jpg)

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