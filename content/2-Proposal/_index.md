---
title: "Proposal"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

{{% notice warning %}}
⚠️ **Note:** The information provided below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

In this section, I present an overview of the workshop planned for the internship program. The content includes system objectives, solution architecture, AWS services utilized, implementation roadmap, budget estimation, risk assessment, and expected outcomes upon completion.

# Retail Operations Monitoring Platform (ROMP)

## Real-time Retail Operations Monitoring Solution on AWS Serverless Platform

---

# 1. Executive Summary

The Retail Operations Monitoring Platform (ROMP) is a retail operations monitoring system built on the **AWS Serverless** architecture. It is designed to automatically track data from existing management systems and detect critical issues during store operations.

Instead of replacing the currently active ERP or POS systems, ROMP acts as an independent **Monitoring Platform**. It connects to the on-premises Oracle database in **Read-Only** mode, periodically analyzes data against defined Business Rules, and dispatches alerts immediately upon detecting anomalies.

Alert notifications are delivered via Amazon SES, while the entire alert history is logged in Amazon DynamoDB for future retrieval and auditing.

The system is designed entirely around an **Event-Driven Architecture**, leveraging AWS Serverless services to reduce operational costs, ensure easy scalability, and eliminate the need to manage underlying server infrastructure.

The primary objective of the project is to build a monitoring platform capable of:

- Monitoring inventory in real time.
- Detecting low-stock items.
- Detecting expired or near-expiration products.
- Monitoring promotion campaign statuses.
- Tracking sales performance.
- Dispatching automated alerts.
- Storing alert history.
- Monitoring system logs and metrics across all components.

---

# 2. Problem Statement

## Current Challenges

In many retail enterprises, legacy ERP or POS systems are heavily focused on transactional operations such as sales, warehousing, or product management. However, these systems generally lack proactive monitoring mechanisms.

Typical pain points include:

- No automatic detection of low-stock products.
- No real-time alerts when items go completely out of stock.
- Failure to proactively spot products nearing their expiration dates.
- No automated reminders when promotional campaigns are about to end.
- No detection of sudden drops or anomalies in sales volume.
- Managers must perform manual, repetitive data audits.

As the number of physical stores and the volume of data grow, manual tracking becomes highly time-consuming and prone to human error.

Furthermore, modifying the core transactional system directly to add monitoring features poses a significant risk to daily business operations.

Therefore, there is an urgent need for an independent monitoring layer that only reads data from the existing database but is capable of processing and alerting in near real-time.

---

## The Solution

The Retail Operations Monitoring Platform is designed as an isolated, non-intrusive monitoring layer.

The system utilizes Amazon EventBridge to trigger AWS Lambda functions on a periodic schedule. Lambda connects to the Oracle Database using a **Read-Only** credential, retrieves the necessary transaction logs, and applies predefined Business Rules to evaluate operational health.

If an anomaly is detected, the Lambda function will:

- send an email alert via Amazon SES;
- store the alert record in DynamoDB;
- output execution logs to Amazon CloudWatch.

This automated flow ensures that administrators are notified of issues instantly without needing to run manual queries.

---

## Benefits and ROI

Deploying ROMP delivers several high-value outcomes:

- Significantly reduces time spent on manual data checks.
- Facilitates early detection of operational bottlenecks.
- Minimizes revenue loss caused by out-of-stock scenarios.
- Reduces product waste by flagging near-expiration items early.
- Proactively manages the lifecycle of marketing promotions.
- Maintains a permanent audit trail of operational alerts.
- Provides comprehensive system observability through unified logging.

By relying entirely on Serverless services, the operational overhead is minimal, making it highly cost-effective for small and medium-sized enterprises (SMEs).

---

# 3. Solution Architecture

ROMP is built using an Event-Driven, Serverless architecture on AWS.

The overall operational flow is as follows:

1. Amazon EventBridge triggers AWS Lambda based on a cron schedule.
2. Lambda connects to the Oracle Database.
3. Oracle serves data exclusively in Read-Only mode.
4. Lambda evaluates the data against Business Rules.
5. If an anomaly is found:
   - sends an Email notification via Amazon SES;
   - saves the alert history to DynamoDB.
6. CloudWatch aggregates all logs and system metrics.

This decoupled design ensures that individual modules operate independently, scale effortlessly, and keep operating costs to a minimum.

![ROMP Architecture](/images/2-Proposal/romp.jpg)

---

## AWS Services Utilized

**Amazon EventBridge**

Orchestrates and schedules periodic invocations of the Lambda functions.

**AWS Lambda**

Executes the core business logic of the platform.

The Lambda functions are modularized into specific microservices:

- Inventory Monitoring
- Expiry Monitoring
- Promotion Monitoring
- Sales Monitoring

**Amazon SES**

Sends automated email alerts to administrators and managers.

**Amazon DynamoDB**

A NoSQL database used to log and store alert histories.

**Amazon CloudWatch**

Collects application logs, performance metrics, and supports system monitoring.

**AWS IAM**

Manages access control and permissions adhering strictly to the Principle of Least Privilege.

**Oracle Database**

The core enterprise data source. 

The monitoring Lambda holds strictly SELECT-only permissions.

---

## Component Design

The platform is segregated into decoupled monitoring modules.

### Inventory Monitoring

Tracks warehouse and shelf stock levels.

Business Rules:

- Quantity = 0 → Out Of Stock
- Quantity ≤ Safety Stock → Low Stock

### Expiry Monitoring

Inspects product shelf-life and expiration dates.

Business Rules:

- Expired.
- Near Expiration.

### Promotion Monitoring

Tracks the status and validity of promotional campaigns.

Business Rules:

- Ending Soon.
- Expired/Inactive.

### Sales Monitoring

Monitors daily sales velocity and volume.

Business Rules:

- Sudden Drop in Sales.
- Sales Volume Exceeds Threshold.

Each module is deployed as an independent Lambda function to ensure ease of maintenance, updating, and isolated scaling.

---

# 4. Technical Implementation

The development process of the system is divided into sequential phases.

## Phase 1

Requirement gathering and architecture design.

This involves:

- studying the AWS Well-Architected Framework;
- designing the Serverless architecture topology;
- defining the functional Business Rules.

---

## Phase 2

Setting up the AWS environment.

This involves:

- creating IAM Roles with least privileges;
- configuring SES identities;
- provisioning DynamoDB tables;
- setting up CloudWatch log groups;
- configuring EventBridge schedulers;
- deploying placeholder Lambda functions.

---

## Phase 3

Establishing Oracle Database connectivity.

This involves:

- building the Oracle connection service;
- conducting network and security connectivity tests;
- executing Read-Only sample queries.

---

## Phase 4

Developing Business Rule engines.

Writing specific processing logic for each decoupled Lambda function module.

---

## Phase 5

End-to-End system testing.

This involves:

- Unit Testing;
- Integration Testing;
- End-to-End (E2E) testing of the alert pipeline.

---

# 5. Budget Estimation

Since the project leverages Serverless services, costs are primarily driven by execution requests and storage size rather than idle idle-server hourly fees.

Estimated monthly costs when operating within the AWS Free Tier limit:

| Service | Cost |
|----------|---------|
| AWS Lambda | Virtually free |
| Amazon DynamoDB | Covered by Free Tier |
| Amazon SES | Negligible cost |
| Amazon EventBridge | Covered by Free Tier |
| Amazon CloudWatch | Covered by Free Tier |
| AWS IAM | Free |

The total estimated operational cost is only a few USD per month if the system slightly exceeds the Free Tier limits.

---

# 6. Risk Assessment

## Risk Matrix

| Risk | Impact | Probability |
|---------|---------------|-----------|
| Oracle database connection failure | High | Medium |
| SES email identity not verified | Medium | Medium |
| Incorrect Business Rule logic | High | Low |
| Exceeding the AWS Free Tier budget | Medium | Low |
| Lambda execution runtime errors | High | Medium |

---

## Mitigation Strategies

- Utilize strictly Read-Only credentials to avoid data corruption.
- Thoroughly unit-test each Lambda function independently.
- Configure active monitoring and alerts in CloudWatch Logs.
- Setup AWS Budget alerts to monitor resource spending.
- Enforce IAM Least Privilege access controls across all services.

---

## Contingency Plan

If a Lambda execution fails:

- EventBridge will trigger the function again during the next scheduled cycle.
- CloudWatch preserves detailed execution logs for post-mortem debugging.
- Lambda functions can be redeployed or updated without causing any downtime or disruption to the main Oracle database.

---

# 7. Expected Outcomes

Upon the successful completion of this workshop, the system is expected to deliver the following achievements:

- Successfully deploy a production-ready retail operations monitoring platform built on AWS Serverless.
- Automatically detect anomalies and threshold breaches within the Oracle Database.
- Dispatch email alerts in near real-time.
- Persist structured alert records in DynamoDB.
- Maintain comprehensive observability of application health using CloudWatch.
- Demonstrate modern Event-Driven design patterns aligned with the AWS Well-Architected Framework.
- Provide a modular blueprint that allows the enterprise to append more monitoring modules in the future without altering the core infrastructure.

Through this project, the student will not only master the practical application of AWS Serverless technologies but also gain critical experience in designing a robust, enterprise-grade monitoring system, laying a solid foundation for building larger Cloud-Native platforms in the future.