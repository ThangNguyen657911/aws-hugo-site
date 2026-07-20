---
title: "Worklog Week 9"
date: 2026-06-22
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}


### Objectives for Week 9:

* Research and deploy high-performance file storage solutions that are fully compatible with popular file systems using Amazon FSx.
* Study and implement large-scale, ultra-low-latency NoSQL databases with Amazon DynamoDB, while understanding long-term cost optimization mechanisms using AWS Savings Plans.
* Explore the powerful serverless data analytics duo for unstructured and semi-structured data: AWS Glue (ETL pipeline) and Amazon Athena (serverless querying using standard SQL).

### Tasks to be Deployed This Week:
| Day | Task | Start Date | End Date | Resource Links |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | ---------- | ----------------------------------------- |
| 2 | - **Amazon FSx:** <br>&emsp; + Study the theoretical concepts of Amazon FSx and its common file system deployment options (FSx for Windows File Server, FSx for Lustre, FSx for NetApp ONTAP) <br>&emsp; + Compare performance characteristics and use cases between Amazon EFS and Amazon FSx | 28/06/2026 | 28/06/2026 | <https://docs.aws.amazon.com/> |
| 3 | - **Hands-on Amazon FSx & DynamoDB:** <br>&emsp; + Create and configure an Amazon FSx for Windows File Server system, and mount it to a Windows EC2 instance <br>&emsp; + Study the core concepts of Amazon DynamoDB: Partition Key, Sort Key, and Read/Write Capacity Modes (On-Demand vs. Provisioned) | 29/06/2026 | 29/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **Hands-on Amazon DynamoDB & AWS Savings Plans:** <br>&emsp; + Create a DynamoDB Table and perform basic CRUD operations (Create, Read, Update, Delete) via the AWS Console and CLI <br>&emsp; + Research cost-optimization mechanisms with AWS Savings Plans: Compare Compute Savings Plans, EC2 Instance Savings Plans, and SageMaker Savings Plans | 30/06/2026 | 30/06/2026 | <https://docs.aws.amazon.com/> |
| 5 | - **AWS Glue:** <br>&emsp; + Learn the architecture of AWS Glue: Data Catalog, Crawlers, Connections, and Glue ETL Jobs <br>&emsp; + Study how AWS Glue automatically discovers data, extracts schema, and transforms data formats (e.g., converting CSV to Parquet) | 01/07/2026 | 01/07/2026 | <https://docs.aws.amazon.com/> |
| 6 | - **Amazon Athena:** <br>&emsp; + Understand the operational principles of Amazon Athena - a serverless solution to query data directly in Amazon S3 using standard SQL without managing infrastructure <br>&emsp; + Research methods to optimize query performance and reduce costs (Data Partitioning, compression, and columnar formats like Parquet/ORC) | 02/07/2026 | 02/07/2026 | <https://docs.aws.amazon.com/> |
| 7 | - **Hands-on AWS Glue & Amazon Athena Integration:** <br>&emsp; + Set up an AWS Glue Crawler to scan a raw dataset (CSV format) stored on Amazon S3 and automatically populate the schema into the Glue Data Catalog <br>&emsp; + Use Amazon Athena to run standard SQL queries directly on the table defined in the Data Catalog | 03/07/2026 | 03/07/2026 | <https://cloudjourney.awsstudygroup.com/> |


### Key Achievements for Week 9:

* **Regarding Amazon FSx:**
  * Mastered practical scenarios for selecting storage solutions: utilizing *FSx for Windows File Server* for native Windows applications integrated with Active Directory, and *FSx for Lustre* for High-Performance Computing (HPC) and machine learning workloads requiring massive throughput.
  * Successfully deployed an FSx Windows file system, mounted it seamlessly to an EC2 instance, and gained a clear understanding of file-level security management (NTFS permissions).

* **Regarding Amazon DynamoDB & Savings Plans:**
  * Gained a comprehensive understanding of DynamoDB's data distribution mechanism using Partition Keys, and how to design secondary indexes (Local Secondary Index - LSI, Global Secondary Index - GSI) to optimize query performance for real-world application workflows.
  * Learned how to use *AWS Cost Explorer* to analyze historical compute usage, enabling data-driven recommendations to purchase a *Savings Plans* commitment (saving up to 72% compared to On-Demand rates) based on a consistent hourly spend over a 1- or 3-year term.

* **Regarding AWS Glue & Amazon Athena:**
  * Mastered the modern serverless data analytics pipeline architecture. Understood the critical role of the *AWS Glue Data Catalog* as a centralized metadata repository for managing cloud data structures.
  * Successfully built and operated an end-to-end data analytics workflow: Configured an **AWS Glue Crawler** to automatically discover and extract metadata schemas from raw CSV files in S3, and utilized **Amazon Athena** to execute complex SQL queries (SELECT, WHERE, GROUP BY) on top of the cataloged tables with millisecond-range response times—all without provisioning a single database server.