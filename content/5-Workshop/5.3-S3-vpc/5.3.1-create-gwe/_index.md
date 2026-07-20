---
title: "Configure Lambda"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3.1 </b> "
---

## Using AWS Lambda

In this section, you will create an AWS Lambda function through the AWS Console, attach the IAM Role prepared in **Section 5.1**, configure the appropriate runtime, memory, and timeout settings, and deploy the Inventory monitoring code from your local machine to AWS.

---

![overview](/images/5-Workshop/5.3-S3-vpc/Lambda1.jpg)

* Verify that the AWS Region is set to:

```
ap-southeast-1 (Singapore)
```

* In the AWS Console search bar, type **Lambda** and open the **Lambda** service.

* Click **Create function**.

---

![overview](/images/5-Workshop/5.3-S3-vpc/Lambda2.jpg)

Configure the Lambda function:

* Select **Author from scratch**.

* **Function name**

```
romp-inventory
```

* **Runtime**

Select:

```
Python 3.12
```

* Scroll down and click **Create function**.

---

![overview](/images/5-Workshop/5.3-S3-vpc/Lambda3.jpg)

After the function has been created:

* Open the newly created Lambda function.

* Select the **Configuration** tab.

* Scroll down to the **Permissions** section.

* Click **Edit**.

---

![overview](/images/5-Workshop/5.3-S3-vpc/Lambda4.jpg)

Configure the execution settings:

* **Memory**

```
512 MB
```

* **Timeout**

```
30 seconds
```

* Under **Existing role**, select:

```
ROMP-Lambda-ExecutionRole
```

* Click **Save**.

---

![overview](/images/5-Workshop/5.3-S3-vpc/Lambda5.jpg)

* Select the **Code** tab.

* Scroll down to **Runtime settings**.

* Click **Edit**.

---

![overview](/images/5-Workshop/5.3-S3-vpc/Lambda6.jpg)

* Enter the **Handler** that matches your Lambda source code.

* Click **Save**.