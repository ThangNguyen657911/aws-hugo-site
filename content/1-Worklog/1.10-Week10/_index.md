---
title: "Worklog Week 10"
date: 2026-07-06
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

### Week 10 Goals:

* The main objective for this week is to finalize the overall architecture design of the Retail Operations Monitoring Platform (ROMP) project on AWS. Work focuses on researching Serverless and Event-Driven architectures, defining the roles of individual AWS services, and constructing architectural diagrams to clearly demonstrate the processing flow and component relationships within the system.

### Tasks to be deployed this week:

| Week | Task | Start Date | Completion Date | Reference Documentation |
| --- | --- | --- | --- | --- |
| 10 | Research business requirements for the retail operations monitoring system and define the scope of the ROMP project. | 06/07/2026 | 11/07/2026 | |
| 10 | Study Serverless and Event-Driven Architecture on AWS to select an appropriate deployment model. | 06/07/2026 | 11/07/2026 | |
| 10 | Research core AWS service functions and roles (AWS Lambda, Amazon EventBridge, Amazon CloudWatch). | 06/07/2026 | 11/07/2026 | |
| 10 | Research storage and notification services (Amazon DynamoDB, Amazon SES, AWS IAM). | 06/07/2026 | 11/07/2026 | |
| 10 | Design the overall system architecture (High-Level Architecture - HLA) for ROMP, detailing component interactions. | 10/07/2026 | 11/07/2026 | |
| 10 | Finalize architecture design documentation, draw Data Flow Diagrams (DFD), and summarize Week 10 tasks. | 06/07/2026 | 11/07/2026 | |

### Week 10 Achievements:

* Successfully completed the architecture diagram set for the ROMP project, accurately reflecting system structure and data processing workflows.
* Selected a Serverless model integrated with Event-Driven architecture to optimize operational costs and overall flexibility.
* Clearly defined AWS service roles in the workflow: EventBridge triggers periodically Lambda executes Business Rules & queries Oracle DB  Logs to CloudWatch, stores history in DynamoDB, and sends email notifications via SES.
* Designed the system architecture with decoupled components to ensure scalability, ease of maintenance, and compliance with the AWS Well-Architected Framework.