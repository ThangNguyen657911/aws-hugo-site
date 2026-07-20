---
title : "CloudWatch with EventBridge"
date : 2024-01-01 
weight : 4 
chapter : false
pre : " <b> 5.4. </b> "
---

#### Overview

In the architecture of the Retail Operations Monitoring Platform (ROMP), the system is built following a Serverless and Event-Driven model, in which Amazon EventBridge and Amazon CloudWatch are two crucial services that help automate the monitoring workflow and track overall system activity.

Amazon EventBridge acts as the system's Scheduler and event orchestrator. Instead of requiring users or administrators to run programs manually, EventBridge triggers AWS Lambda functions on a configured schedule, such as every 5 minutes or 15 minutes. When execution time arrives, EventBridge sends an Event to Lambda, prompting it to connect to the Oracle database, gather data, and execute Business Rules to detect anomalies such as low stock, out-of-stock items, products nearing expiration, or promotions about to end. This mechanism enables fully automated operation, ensuring continuous monitoring without manual intervention.

Once Lambda is triggered and completes its processing, all execution details are recorded in Amazon CloudWatch. CloudWatch serves as the system monitoring and tracking service, storing logs and aggregating execution counts, processing duration, as well as Lambda success and error rates. This information allows the operations team to quickly identify root causes when issues arise while evaluating system performance over time.

The combination of EventBridge and CloudWatch creates a closed-loop operational workflow. EventBridge handles scheduled task triggers, while CloudWatch monitors and logs the entire execution process. Consequently, ROMP can operate autonomously, monitor continuously, and provide comprehensive data for system auditing, maintenance, and optimization.

####  [5.4.1 CloudWatch Configuration](5.4.1-prepare/)
####  [5.4.2 EventBridge Configuration](5.4.2-create-interface-enpoint/)