---
title: "Worklog Week 5"
date: 2026-05-25
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}


### Objectives for Week 5:

* Learn and apply the Serverless computing model with **AWS Lambda** to automate system administration tasks based on conditions or schedules.
* Explore advanced monitoring visualization solutions by integrating **Grafana** with AWS data sources (such as Amazon CloudWatch).
* Master resource classification and centralized large-scale management strategies using **AWS Tagging Best Practices** and **AWS Resource Groups**.

### Tasks to Implement This Week:
| Day | Task | Start Date | End Date | Resource Links |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | ---------- | ----------------------------------------- |
| 2 | - **AWS Lambda Automation (Theory):** <br>&emsp; + Understand Serverless computing concepts and how AWS Lambda works <br>&emsp; + Learn about the Event-driven programming model and how Lambda integrates with Amazon EventBridge (CloudWatch Events) for scheduled automation | 31/05/2026 | 31/05/2026 | <https://docs.aws.amazon.com/> |
| 3 | - **AWS Lambda Automation Hands-on:** <br>&emsp; + Write a simple Lambda function in Python (using the `boto3` library) to automatically shut down unused EC2 Instances at the end of the day to optimize costs <br>&emsp; + Configure an EventBridge Rule as a trigger to run the Lambda periodically | 01/06/2026 | 01/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **Grafana (Theory & Setup):** <br>&emsp; + Study the overview of Grafana and its visualization advantages over the default CloudWatch Dashboard <br>&emsp; + Research deployment options for Grafana (self-hosted on EC2 or using Amazon Managed Grafana) | 02/06/2026 | 02/06/2026 | <https://docs.aws.amazon.com/> |
| 5 | - **Grafana & CloudWatch Integration Hands-on:** <br>&emsp; + Configure an IAM Role/Policy to grant Grafana permission to read metrics from CloudWatch <br>&emsp; + Add CloudWatch as a Data Source in Grafana and design a professional EC2 monitoring Dashboard with highly customized panels | 03/06/2026 | 03/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - **AWS Tagging & Resource Groups (Theory):** <br>&emsp; + Study Tagging Best Practices for cost allocation, Attribute-Based Access Control (ABAC), and operations management <br>&emsp; + Understand AWS Resource Groups to organize resources by project/environment | 04/06/2026 | 04/06/2026 | <https://docs.aws.amazon.com/> |
| 7 | - **Resource Management with Tagging & Resource Groups Hands-on:** <br>&emsp; + Use the Tag Editor tool to bulk tag active running resources <br>&emsp; + Create a query-based Resource Group based on tags to centrally manage and track the health of all resources belonging to a specific project | 05/06/2026 | 05/06/2026 | <https://cloudjourney.awsstudygroup.com/> |


### Key Achievements in Week 5:

* **AWS Lambda Automation:**
  * Gained a deep understanding of the Serverless paradigm, completely eliminating the overhead of managing or patching underlying operating systems and dynamically optimizing computing power based on real-time demand.
  * Successfully wrote and deployed a Python function using the **Boto3 SDK** to inspect running states and shut down EC2 Instances tagged with `Environment: Development` at 19:00 daily.
  * Successfully connected the Lambda function to an **Amazon EventBridge Rule** (using Cron expressions), allowing the system to run automatically without manual intervention, saving up to 30% on non-business hour server costs.

* **Grafana:**
  * Evaluated the flexibility of Grafana in consolidating, visualizing, and querying multi-source data within a single, unified dashboard interface.
  * Successfully configured a secure connection between Grafana and AWS by setting up a restricted IAM Role (allowing only read-only permissions for CloudWatch metrics with `CloudWatchReadOnlyAccess`).
  * Built a fully operational **Grafana Dashboard** that dynamically visualizes key EC2 metrics (CPU Utilization, Network In/Out, Disk Read/Write) with distinct threshold color-coding, making it far more intuitive than the default CloudWatch UI.

* **AWS Tagging & Resource Groups:**
  * Established a standardized Tagging Schema for the internship environment, incorporating mandatory tags such as: `Project`, `Environment`, `Owner`, and `CostCenter`.
  * Successfully used the **Tag Editor** within AWS Resource Groups to quickly search and modify/add tags in bulk to previously untagged active resources (EC2, S3, RDS, Security Groups).
  * Created a **Query-based Resource Group** that groups all resources sharing the tag `Project: FirstCloudAI`. From the Resource Groups console, easily monitored the health, configuration, and active CloudWatch Alarms associated with this specific project without navigating through individual services.