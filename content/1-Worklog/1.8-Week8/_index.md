---
title: "Worklog Week 8"
date: 2026-06-15
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy it word-for-word** for your report, including this warning.
{{% /notice %}}


### Objectives for Week 8:

* Study containerization technology with Docker, how to build and optimize Dockerfiles, and manage container application lifecycles.
* Research container orchestration solutions using Amazon ECS (Elastic Container Service) running on the AWS Fargate serverless environment.
* Build a fully automated Continuous Integration and Continuous Deployment (CI/CD) pipeline using AWS CodePipeline.
* Understand hybrid cloud storage integration mechanisms between On-Premises infrastructure and AWS via AWS Storage Gateway.

### Tasks to be Deployed This Week:
| Day | Task | Start Date | Completion Date | Reference Resource |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| 2 | - **Docker & Containerization:** <br>&emsp; + Learn the theoretical aspects of Containers and the differences between Virtual Machines (VMs) and Containers <br>&emsp; + Master basic Docker commands: build, run, push/pull, volume, and network | 21/06/2026 | 21/06/2026      | <https://docs.docker.com/> |
| 3 | - **Docker & AWS ECR Practice:** <br>&emsp; + Write a Dockerfile to package a simple web application (Node.js/Python) <br>&emsp; + Create a Private Repository on Amazon ECR (Elastic Container Registry) <br>&emsp; + Push the Docker image to Amazon ECR | 22/06/2026 | 22/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **Amazon ECS & AWS Fargate:** <br>&emsp; + Study Amazon ECS architecture and its core concepts: Task Definition, Task, Service, and Cluster <br>&emsp; + Differentiate between running ECS on EC2 versus Serverless with AWS Fargate | 23/06/2026 | 23/06/2026      | <https://docs.aws.amazon.com/> |
| 5 | - **Amazon ECS & CI/CD with AWS CodePipeline Practice:** <br>&emsp; + Create an ECS Fargate Cluster and configure a Task Definition pointing to the ECR image <br>&emsp; + Set up AWS CodePipeline (connecting CodeCommit/GitHub -> CodeBuild -> CodeDeploy) to automatically deploy new container versions upon source code changes | 24/06/2026 | 24/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - **AWS Storage Gateway:** <br>&emsp; + Explore hybrid cloud storage models and solutions for synchronizing local data to the Cloud <br>&emsp; + Study different gateway types: S3 File Gateway, Volume Gateway, and Tape Gateway | 25/06/2026 | 25/06/2026      | <https://docs.aws.amazon.com/> |
| 7 | - **AWS Storage Gateway Practice:** <br>&emsp; + Learn the deployment workflow of the Storage Gateway VM within a virtualized On-Premises environment <br>&emsp; + Simulate associating an S3 File Gateway with an Amazon S3 bucket to share files via NFS/SMB network protocols | 26/06/2026 | 26/06/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Achievements in Week 8:

* **Docker & Amazon ECR:**
  * Mastered the workflow of packaging independent applications, completely resolving environmental discrepancy issues between Local and Production environments.
  * Successfully wrote an optimized **Dockerfile** (using multi-stage builds), created a Private Repository on **Amazon ECR**, configured IAM-based access control, and pushed the Docker Image to the registry securely.

* **Amazon ECS & AWS Fargate:**
  * Gained a deep understanding of the Serverless Container model. AWS Fargate completely removes the operational burden of managing, patching underlying EC2 host operating systems, and configuring server scaling.


  * Successfully deployed a web application running on **Amazon ECS** as **AWS Fargate Tasks**. Configured the system to run stably behind an Application Load Balancer (ALB) and set up automated Health Checks to detect and replace unhealthy containers.

* **AWS CodePipeline (CI/CD):**
  * Built a 100% automated CI/CD pipeline. Every time a new commit is pushed to the source code repository, the system triggers **AWS CodeBuild** to build a new Docker Image, pushes it to ECR, and prompts **AWS CodeDeploy** to perform a rolling update on the ECS Service with Zero Downtime.

* **AWS Storage Gateway:**
  * Cleared up practical use cases for different Storage Gateways. **S3 File Gateway** is optimized for sharing local files directly to S3, **Volume Gateway** provides low-latency block storage backed by EBS Snapshots, and **Tape Gateway** seamlessly replaces long-term physical tape backup systems.

  * Understood the local caching mechanism of **S3 File Gateway**, which allows On-Premises applications to access files with local-like latency while asynchronously and continuously syncing the master data to secure Amazon S3 buckets.