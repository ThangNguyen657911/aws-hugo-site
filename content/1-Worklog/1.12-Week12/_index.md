---
title: "Worklog Week 12"
date: 2026-07-12
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}


### Objectives for Week 12:

* Consolidate all acquired knowledge to design a detailed system architecture and construct a complete data pipeline for the ROMP retail monitoring project.
* Deploy and integrate AWS services in a real-world scenario to realize an automated and intelligent retail monitoring solution.
* Package the product deliverables, finalize technical documentation, prepare the presentation slides, and practice delivery skills to professionally report the project before the evaluation board.

### Tasks to be Deployed This Week:
| Day | Task | Start Date | End Date | Resource Links |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | ---------- | ----------------------------------------- |
| 2 | - **ROMP Project Architecture Design:** <br>&emsp; + Define the overall system architecture of the ROMP (Retail Observation & Monitoring Platform) project <br>&emsp; + Draw data flow diagrams (DFD) tracing from in-store camera/sensor data collection to data processing and visualization | 20/07/2026 | 20/07/2026 | Internal Project Documentation |



### Key Achievements for Week 12:

* **Regarding ROMP Project Design & Architecture:**
  * Successfully aligned and finalized the architecture design of the **ROMP** retail monitoring platform following the *AWS Well-Architected Framework* standards to ensure high availability, security, and cost efficiency.
  * Clearly defined a 3-tier data pipeline (Raw -> Cleaned -> Analytics) to maintain a strict separation between raw storage and downstream analytics exploitation.

* **Regarding Smart Retail System Deployment:**
  * Successfully realized the automated end-to-end data pipeline: Retail data is ingested into **Amazon S3**, indexed automatically via **AWS Glue**, queried at scale using **Amazon Athena**, and visualized dynamically through interactive **Amazon QuickSight** dashboards.
  * Successfully integrated intelligent predictive models from **Amazon SageMaker**, enabling the ROMP platform to provide actionable recommendations for shelf placement optimization based on in-store customer density and foot traffic behaviors.

* **Regarding Project Packaging & Presentation:**
  * Fully packaged the entire project infrastructure as code (IaC) utilizing **AWS SAM** templates, enabling the replication and deployment of the platform to new retail branches within minutes.
  * Completed professional presentation slides and practiced a seamless live-demo script, ensuring full readiness to confidently defend the ROMP retail monitoring project with robust technical evidence before the evaluation board.