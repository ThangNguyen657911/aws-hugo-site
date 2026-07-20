---
title : "EventBridge Configuration"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.4.2 </b> "
---

#### EventBridge Deployment

![name](/images/5-Workshop/5.4-S3-onprem/EB1.jpg)

* Check region: ap-southeast-1 (Singapore).
* In the search bar, type EventBridge → select Amazon EventBridge.
* In the left menu, select Rules.
* Click Create rule.

![name](/images/5-Workshop/5.4-S3-onprem/EB2.jpg)

* Name: enter exactly `ROMP-Inventory-Schedule`.
* Description: Triggers romp-inventory Lambda every 5 minutes during development phase.
* Time: you can set this optionally.
* Click Next.

![name](/images/5-Workshop/5.4-S3-onprem/EB3.jpg)

* Schedule pattern: select A schedule that runs at a regular rate.
* Rate expression: enter value 5, select Minutes for unit.
* The console will automatically display a preview as `rate(5 minutes)` — verify it is correct.
* Time: you can set this optionally.
* Click Next.

![name](/images/5-Workshop/5.4-S3-onprem/EB4.jpg)

* Target type: select AWS service.
* Select a target: in the dropdown, type/select Lambda function.
* Function: in the dropdown select function, type `romp-inventory` to filter, then select the deployed function.
* Click Next.

![name](/images/5-Workshop/5.4-S3-onprem/EB5.jpg)

* Add tags `Project = ROMP`, `Module = Inventory`.
* Click Next.

![name](/images/5-Workshop/5.4-S3-onprem/EB6.jpg)

* Review everything:
  * Name: ROMP-Inventory-Schedule
  * Schedule: rate(5 minutes)
  * Target: Lambda romp-inventory
* Click Create rule.

![name](/images/5-Workshop/5.4-S3-onprem/EB7.jpg)

* Status after configuration is completed.