---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

{{% notice warning %}}
⚠️ **Note:** The information provided below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}


# RETAIL OPERATIONS MONITORING PLATFORM (ROMP) WORKSHOP

#### Overview

The Retail Operations Monitoring Platform (ROMP) is a real-time retail operation monitoring solution built on the AWS Serverless architecture and Event-Driven Architecture. ROMP functions as an independent monitoring platform, securely connecting to the enterprise's existing Oracle database in Read-Only mode to proactively analyze operational Business Rules without affecting or disrupting the core systems (ERP/POS).

In this lab, we will build and configure the entire Serverless infrastructure for ROMP. The system will automate the data scanning process, apply business rule sets to detect anomalies (such as low stock, expiring products, or sales fluctuations), thereby automatically logging history and sending instant alerts to administrators.

**Serverless Architecture Services Applied
The workshop will guide you through integrating and configuring a chain of event-driven Cloud-Native services:**

* **Amazon EventBridge:** Acts as the Scheduler to automatically trigger periodic health checks.

* **AWS Lambda:** The core business logic processing hub, decoupled into independent modules such as Inventory, Expiry, Promotion, and Sales Monitoring to optimize maintainability.

* **Amazon DynamoDB:** A Serverless NoSQL database used to store and retrieve the entire history of generated alerts.

* **Amazon SES (Simple Email Service):** The mechanism responsible for sending automated and instant email alerts to management levels upon detecting operational issues.

* **Amazon CloudWatch:** A centralized monitoring system that collects all Logs and Metrics, ensuring system transparency and supporting troubleshooting analysis.

![ROMP Architecture](/images/2-Proposal/romp.jpg)

#### Content

1. [Platform Setup & IAM Permissions](5.1-Workshop-overview/)
2. [Initialize Storage & Notification Channels (DynamoDB & SES)](5.2-Prerequiste/)
3. [Setup Lambda and code Business Rule](5.3-S3-vpc/)
4. [CloudWatch with EventBridge](5.4-S3-onprem/)
5. [End-to-End (E2E) Testing](5.5-Policy/)
6. [Resource Cleanup](5.6-Cleanup/)