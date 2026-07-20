---
title: "Worklog Week 3"
date: 2026-05-11
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}


### Objectives for Week 3:

* Connect and practice secure EC2 instance management without opening security ports or managing SSH keys, using **AWS Systems Manager (SSM)** and **Session Manager**.
* Master system monitoring solutions with **AWS CloudWatch**, configure automated alarms for resource overload, and visualize monitoring data.
* Get familiar with Infrastructure as Code (IaC) methodology via **AWS CloudFormation** to automate resource provisioning.

### Tasks to Implement This Week:
| Day | Task | Start Date | End Date | Resource Links |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | ---------- | ----------------------------------------- |
| 2 | - **AWS Systems Manager & Session Manager (Theory):** <br>&emsp; + Learn about AWS Systems Manager (SSM) and centralized server management <br>&emsp; + Study Session Manager: How to establish secure terminal connections to EC2 without opening port 22 (SSH), needing a Bastion Host, or managing SSH Keys | 17/05/2026 | 17/05/2026 | <https://docs.aws.amazon.com/> |
| 3 | - **SSM & Session Manager Hands-on:** <br>&emsp; + Create an IAM Role with the `AmazonSSMManagedInstanceCore` policy attached to the EC2 instance <br>&emsp; + Launch an EC2 Instance with SSM Agent pre-installed and verify secure shell connection via Session Manager on the AWS Console | 18/05/2026 | 18/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **AWS CloudWatch (Theory):** <br>&emsp; + Study core components of CloudWatch: Metrics, Logs, Alarms, and Dashboards <br>&emsp; + Differentiate between Basic Monitoring and Detailed Monitoring | 19/05/2026 | 19/05/2026 | <https://docs.aws.amazon.com/> |
| 5 | - **CloudWatch Monitoring & Alarms Hands-on:** <br>&emsp; + Install CloudWatch Agent on EC2 to collect system logs and RAM metrics <br>&emsp; + Set up CloudWatch Alarms integrated with Amazon SNS to send automatic email alerts when CPU usage exceeds 80% <br>&emsp; + Build a visual Dashboard to monitor system resources | 20/05/2026 | 20/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - **AWS CloudFormation (Theory):** <br>&emsp; + Understand the concept of Infrastructure as Code (IaC) and the benefits of infrastructure automation <br>&emsp; + Analyze the structure of a CloudFormation template (YAML/JSON) including: Parameters, Resources, Outputs | 21/05/2026 | 21/05/2026 | <https://docs.aws.amazon.com/> |
| 7 | - **CloudFormation Hands-on:** <br>&emsp; + Author a basic YAML template to automatically deploy an EC2 Instance inside a custom Security Group <br>&emsp; + Execute creation, update, and deletion of Stacks on the CloudFormation console to understand the rollback mechanism | 22/05/2026 | 22/05/2026 | <https://cloudjourney.awsstudygroup.com/> |


### Key Achievements in Week 3:

* **AWS Systems Manager & Session Manager:**
  * Understood the underlying mechanism of the SSM Agent running inside the instance, allowing AWS to manage the OS remotely and securely through internal AWS APIs instead of exposing network ports to the public Internet.
  * Successfully practiced connecting directly to the EC2 instance's command line (shell) via **Session Manager** in the browser. This eliminated the need for Public IPs, opening port 22 (SSH) in Security Groups, and managing key pair (.pem) files, greatly reducing the attack surface.

* **AWS CloudWatch:**
  * Gained a solid understanding of how CloudWatch collects metrics from AWS services under default intervals (5 minutes for basic) or granular intervals (1 minute for detailed).
  * Successfully installed **CloudWatch Agent** on the EC2 instance to collect metrics that the hypervisor cannot natively read (such as RAM utilization and disk space availability) and pushed them to the CloudWatch console.
  * Configured an automated alerting system: When performing a simulated CPU stress test, the system detected the threshold breach, triggered a CloudWatch Alarm, and successfully dispatched an `ALARM` state email notification to the administrator via **Amazon SNS (Simple Notification Service)**.
  * Designed a real-time **CloudWatch Dashboard** to visually track CPU, RAM, and Disk Space usage in one central place.

* **AWS CloudFormation:**
  * Adopted the Infrastructure as Code (IaC) mindset, realizing how to package and version-control infrastructure within a single template file to easily spin up identical environments (Dev, Staging, Production) consistently.
  * Authored a clean **YAML** template defining input properties (Parameters), declaring resources to provision (Resources), and returning critical values such as the Instance ID or Public DNS in the Outputs section.
  * Familiarized with the Stack Lifecycle: Understood CloudFormation's error handling mechanism where a failed resource creation automatically triggers a `Rollback` process, deleting all previously created resources to return the stack to a clean, original state.