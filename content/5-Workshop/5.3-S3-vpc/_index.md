---
title : "Lambda Configuration and Business Rule Code"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### AWS Lambda Configuration and Business Rule Deployment
After completing the infrastructure setup steps such as IAM Role, Amazon EventBridge, Amazon SES, and Amazon DynamoDB, the next step is to build AWS Lambda to monitor data from the Oracle system and process business rules.

AWS Lambda serves as the central processing component of the ROMP system. Lambda is triggered on a recurring schedule by Amazon EventBridge, then connects to the Oracle database in Read Only mode to retrieve data for monitoring. Based on predefined business rules, Lambda analyzes the data, identifies cases requiring alerts, and executes corresponding actions such as sending notification emails via Amazon SES, saving alert history into Amazon DynamoDB, and logging execution to Amazon CloudWatch.



#### Business Rule Deployment

Business Rules are the most critical component of ROMP as they determine when the system generates alerts. Instead of simply fetching data from Oracle, Lambda evaluates each record against predefined business conditions.

For the Inventory Monitoring module, the system checks the inventory quantity (`quantity`) of each product and compares it with the safety stock threshold (`safety_stock`). The processing rules are structured as follows:

If `quantity` = 0, the product is identified as Out of Stock, and the system generates a high-severity alert.
If 0 < `quantity` ≤ `safety_stock`, the product is identified as Low Stock, and the system generates a replenishment alert.
If `quantity` > `safety_stock`, the product is considered Normal, and the system only records the result without generating an alert.

When an alert is detected, Lambda executes the following steps sequentially:

* Read data from Oracle Database.
* Evaluate against Business Rules.
* Generate alert content.
* Send email via Amazon SES.
* Save alert history into Amazon DynamoDB.
* Log and record execution metrics on Amazon CloudWatch.

Thanks to this automated processing mechanism, ROMP can continuously monitor inventory status without manual intervention, helping businesses detect stock shortage risks early and make timely replenishment decisions.




####  [5.3.1 Lambda Configuration](5.3.1-create-gwe/)
####  [5.3.2 Code Business Rule](5.3.2-test-gwe/)