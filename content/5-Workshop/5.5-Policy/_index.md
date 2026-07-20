---
title : "Results Achieved"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---

### Verify results after implementation

#### Verify Lambda

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ1.jpg)

* In the search bar, select Lambda.
* Select Functions on the left menu.
* Select the function `romp-inventory`.

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ2.jpg)

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ3.jpg)

* Select the Code tab.
* Select Upload from.
* Select Choose file.
* At this step, upload the packaged `.zip` file created in section [5.3.2](5.3.2-test-gwe/).
* Click Save.

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ4.jpg)

* Click Test.
* View the output result in the Lambda console.

#### Verify EventBridge and SES

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ5.jpg)

* Next, open the email configured to receive notifications.
* Result achieved for **EventBridge**: Automatically checks the database every 5 minutes and updates alerts for items that are out of stock or low in stock.
* Result achieved for **SES**: Successfully sends emails when the Business Rule in Lambda triggers an alert.
* Email sending interval can be customized.

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ6.jpg)

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ7.jpg)

* Content of the alert email received.

#### Verify DynamoDB

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ11.jpg)

* In the search bar, type DynamoDB.
* Select Tables.
* Select `ROMP-AlertHistory`.

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ12.jpg)

* Click Explore table items.

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ8.jpg)

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ9.jpg)

* Results saved into DynamoDB.

#### Verify CloudWatch

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ13.jpg)

* In the search bar, type CloudWatch.
* Select Log groups under Log Management.
* Select `/aws/lambda/romp-inventory`.

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ14.jpg)

* Select the latest log stream.

![endpoint diagram](/images/5-Workshop/5.5-Policy/KQ10.jpg)

* Recorded execution logs in CloudWatch.