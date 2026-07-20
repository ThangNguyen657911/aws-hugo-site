---
title: "Worklog Week 4"
date: 2026-05-18
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}


### Objectives for Week 4:

* Learn and understand how to migrate on-premises virtualized systems to the cloud using the automated **VM Import/Export** tool.
* Master the process of heterogeneous database schema migration (migrating between different database engines) using the **AWS Schema Conversion Tool (SCT)**.
* Practice configuring and deploying **AWS Database Migration Service (DMS)** to migrate data securely and continuously while minimizing system downtime.

### Tasks to Implement This Week:
| Day | Task | Start Date | End Date | Resource Links |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | ---------- | ----------------------------------------- |
| 2 | - **AWS VM Import/Export (Theory & Preparation):** <br>&emsp; + Learn the concepts and architecture of migrating virtual machines (VMs) from on-premises environments (VMware, Hyper-V) to AWS EC2 <br>&emsp; + Understand supported virtual disk formats (OVA, VMDK, VHD) and configure the required IAM Role (`vmimport`) | 24/05/2026 | 24/05/2026 | <https://docs.aws.amazon.com/> |
| 3 | - **VM Import/Export Hands-on:** <br>&emsp; + Create an S3 Bucket and upload a sample virtual disk file <br>&emsp; + Use the AWS CLI to execute the `aws ec2 import-image` command to convert the virtual disk file into a bootable Amazon Machine Image (AMI) <br>&emsp; + Monitor the import progress via CLI | 25/05/2026 | 25/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **AWS Schema Conversion Tool (SCT) - Theory & Installation:** <br>&emsp; + Learn the workflow of converting database schemas across different database engines (e.g., Microsoft SQL Server to Amazon Aurora/PostgreSQL) <br>&emsp; + Download and install AWS SCT on a local workstation along with the required database drivers | 26/05/2026 | 26/05/2026 | <https://docs.aws.amazon.com/> |
| 5 | - **Schema Conversion with SCT Hands-on:** <br>&emsp; + Initialize an AWS SCT project, and connect to both source and target database engines <br>&emsp; + Run an Assessment Report to analyze schema compatibility and identify elements requiring manual optimization <br>&emsp; + Perform schema conversion and apply the new schema to the target database | 27/05/2026 | 27/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - **AWS Database Migration Service (DMS) - Theory:** <br>&emsp; + Study the core architecture of AWS DMS: Replication Instances, Source/Target Endpoints, and Replication Tasks <br>&emsp; + Differentiate between migration modes: Full Load, Full Load + CDC (Change Data Capture), and CDC-only | 28/05/2026 | 28/05/2026 | <https://docs.aws.amazon.com/> |
| 7 | - **AWS DMS Hands-on:** <br>&emsp; + Provision an AWS DMS Replication Instance and establish secure endpoint connections to both source and target databases <br>&emsp; + Create and trigger a Database Migration Task (Full Load) to synchronize data <br>&emsp; + Monitor the migration task progress directly on the AWS DMS Console | 29/05/2026 | 29/05/2026 | <https://cloudjourney.awsstudygroup.com/> |


### Key Achievements in Week 4:

* **AWS VM Import/Export:**
  * Mastered the systematic process of migrating physical servers or on-premises virtual machines to the AWS cloud environment.
  * Successfully set up the `vmimport` Service Role with precise trust policies, allowing the VM Import/Export service to securely access virtual disk files stored in the designated S3 Bucket.
  * Successfully imported a sample virtual disk image from Amazon S3 into an **Amazon Machine Image (AMI)** using the AWS CLI. Practiced monitoring the status of the import process through the `active`, `converting`, and `completed` states.

* **AWS Schema Conversion Tool (SCT):**
  * Understood the critical role of SCT in heterogeneous database migrations where source and target database engines have fundamentally different architectures.
  * Installed the AWS SCT application locally and configured the necessary connectivity database drivers (JDBC Drivers) for both source and target engines.
  * Generated a **Database Migration Assessment Report** in PDF format, which analyzed the schema and pinpointed code elements (such as complex Stored Procedures or Triggers) that could not be auto-converted, allowing for accurate manual effort estimation.
  * Successfully converted structural tables, constraints, and indexes from the source database engine and applied them to the target schema.

* **AWS Database Migration Service (DMS):**
  * Mastered the core components of the AWS DMS architecture, including the intermediary **Replication Instance**, **Source/Target Endpoints**, and **Replication Tasks**.
  * Configured and verified connections for both Source and Target Endpoints, successfully passing the DMS connection tests.
  * Executed a **Full Load** database migration task, verified data integrity on the target database post-migration, and learned how to configure **Change Data Capture (CDC)** to continuously replicate real-time data changes from the source database without interrupting active production workloads.