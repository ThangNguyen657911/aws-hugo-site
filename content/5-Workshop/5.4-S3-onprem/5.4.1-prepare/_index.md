---
title : "CloudWatch Configuration"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---

#### CloudWatch Deployment

![route 53 diagram](/images/5-Workshop/5.4-S3-onprem/CW1.jpg)

* Check the region: ensure you are still in ap-southeast-1 (Singapore).
* In the search bar, type CloudWatch → select CloudWatch.
* In the left menu, select Log groups (under the Logs section).
* Click Create log group.

![route 53 diagram](/images/5-Workshop/5.4-S3-onprem/CW2.jpg)

* Log group name: enter exactly `/aws/lambda/romp-inventory`.
* Retention setting: click the dropdown, select 30 days.

![route 53 diagram](/images/5-Workshop/5.4-S3-onprem/CW3.jpg)

* Tags (optional): add `Project = ROMP`, `Module = Inventory` if desired.
* Click Create.

![route 53 diagram](/images/5-Workshop/5.4-S3-onprem/CW4.jpg)

* Status after the configuration is complete.