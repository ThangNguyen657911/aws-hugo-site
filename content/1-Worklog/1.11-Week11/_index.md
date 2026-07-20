---
title: "Worklog Week 11"
date: 2026-07-13
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

### Week 11 Goals:

* The main objective for this week is to start deploying the Retail Operations Monitoring Platform (ROMP) system on AWS based on the architecture designed in previous weeks. Concurrently, build the development environment, configure AWS services, and develop the system's first monitoring module (Inventory Monitoring).

### Tasks to be deployed this week:

| Week | Task | Start Date | Completion Date | Reference Documentation |
| --- | --- | --- | --- | --- |
| 11 | Initialize the ROMP project, build the project structure (Layered Architecture), set up Virtual Environment (`.venv`), and install required Python libraries (`boto3`, `oracledb`, `python-dotenv`). | 13/07/2026 | 18/07/2026 | |
| 11 | Configure Oracle Database connection in Read Only mode for secure data retrieval. | 13/07/2026 | 18/07/2026 | |
| 11 | Set up core AWS infrastructure: Configure IAM Role (Least Privilege), create Amazon DynamoDB table for alert history, and verify Amazon SES for email notifications. | 13/07/2026 | 18/07/2026 | |
| 11 | Build AWS Lambda source code for the Inventory Monitoring module (`config`, `logger`, `oracle_service`, `inventory_repository`, `inventory_service`, `handler`, `lambda_function`). | 13/07/2026 | 18/07/2026 | |
| 11 | Implement Business Rules to evaluate product inventory levels (`quantity`) and classify product status: Normal, Low Stock, and Out of Stock. | 13/07/2026 | 18/07/2026 | |
| 11 | Configure Amazon EventBridge to trigger Lambda on a scheduled basis; perform End-to-End testing, and monitor execution logs via Amazon CloudWatch. | 13/07/2026 | 18/07/2026 | |

### Week 11 Achievements:

* Successfully deployed the **Inventory Monitoring** module of the ROMP system on AWS, operating stably and accurately according to the designed architecture.
* Completed an automated end-to-end workflow: Amazon EventBridge scheduled trigger AWS Lambda queries Oracle Database Business Rules process and detect low stock or out-of-stock items.
* Successfully integrated supporting AWS infrastructure services: Send alert emails via Amazon SES, store historical alert records in Amazon DynamoDB, and track operational logs on Amazon CloudWatch.
* Ensured security and governance best practices by configuring IAM Roles using Least Privilege principles and establishing Oracle Database connections in Read Only mode.