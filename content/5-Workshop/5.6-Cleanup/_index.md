---
title : "Clean Up Resources"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

#### Clean Up Resources

Congratulations on successfully completing this lab!

Once you have finished, if you are no longer using these resources, you can clean them up.


#### Cleanup Steps



![hosted zone](/images/5-Workshop/5.6-Cleanup/DD1.jpg)

* In the search bar, type EC2.
* Select Instances.
* Check the box for the instance you want to delete.
* Select Terminate (delete) instance.

![hosted zone](/images/5-Workshop/5.6-Cleanup/DD2.jpg)

* Select Terminate.

![hosted zone](/images/5-Workshop/5.6-Cleanup/DD3.jpg)

* In the search bar, type Lambda.
* Select Functions.
* Check the box for the function you want to delete.
* Select Actions, then select Delete.


![hosted zone](/images/5-Workshop/5.6-Cleanup/DD4.jpg)

* Type `delete` to confirm.
* Select Delete.

![hosted zone](/images/5-Workshop/5.6-Cleanup/DD5.jpg)

* In the search bar, type CloudWatch.
* Select Log groups.
* Check the box for the log group you want to delete.
* Select Actions, then select Delete log group(s).

![hosted zone](/images/5-Workshop/5.6-Cleanup/DD6.jpg)

* Select Delete.

![hosted zone](/images/5-Workshop/5.6-Cleanup/DD7.jpg)

* In the search bar, type EventBridge.
* Select Rules (or Scheduled rules).
* Check the box for the rule you want to delete.
* Select Delete.

![hosted zone](/images/5-Workshop/5.6-Cleanup/DD8.jpg)

* Type `delete` to confirm.
* Select Delete.

![hosted zone](/images/5-Workshop/5.6-Cleanup/DD9.jpg)

* In the search bar, type IAM.
* Select Roles.
* Check the box for the role you want to delete.
* Select Delete.

![hosted zone](/images/5-Workshop/5.6-Cleanup/DD10.jpg)

* Enter the name of the role to confirm.
* Select Delete.