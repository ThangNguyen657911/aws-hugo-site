---
title: "Worklog Week 7"
date: 2026-06-08
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy it word-for-word** for your report, including this warning.
{{% /notice %}}


### Objectives for Week 7:

* Learn about and deploy web application security solutions to protect against common attacks using AWS WAF (Web Application Firewall).
* Research and build an automated, centralized data backup and recovery policy using AWS Backup.
* Learn about and practice advanced networking solutions to connect VPCs using VPC Peering and AWS Transit Gateway.

### Tasks to be Deployed This Week:
| Day | Task | Start Date | Completion Date | Reference Resource |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| 2 | - **AWS WAF (Web Application Firewall):** <br>&emsp; + Learn the theoretical aspects of web application firewalls and the OWASP Top 10 list of common vulnerabilities <br>&emsp; + Understand key concepts: Web ACL, Rules, Rule Groups, and IP Sets | 14/06/2026 | 14/06/2026      | <https://docs.aws.amazon.com/> |
| 3 | - **AWS WAF Practice:** <br>&emsp; + Create a Web ACL and configure basic AWS Managed Rules <br>&emsp; + Test blocking access based on IP addresses (IP Set) or geographic location (Geo-match) <br>&emsp; + Associate WAF with an Application Load Balancer (ALB) or CloudFront | 15/06/2026 | 15/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **AWS Backup:** <br>&emsp; + Study centralized, automated backup solutions and data lifecycle management on AWS <br>&emsp; + Understand core components: Backup Vault, Backup Plan, and Recovery Point | 16/06/2026 | 16/06/2026      | <https://docs.aws.amazon.com/> |
| 5 | - **AWS Backup Practice:** <br>&emsp; + Initialize a Backup Vault and configure a custom Backup Plan <br>&emsp; + Set up automatic backup schedules and lifecycle policies (moving data to Cold Storage after a certain period) for EC2 or RDS resources | 17/06/2026 | 17/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - **VPC Peering & AWS Transit Gateway (TGW):** <br>&emsp; + Study how to establish internal network connectivity between VPCs <br>&emsp; + Compare the pros, cons, and network topologies of traditional full-mesh VPC Peering versus the hub-and-spoke model of Transit Gateway | 18/06/2026 | 18/06/2026      | <https://docs.aws.amazon.com/> |
| 7 | - **VPC Peering Practice:** <br>&emsp; + Create two distinct VPCs and establish a VPC Peering Connection between them <br>&emsp; + Reconfigure Route Tables on both sides and verify connectivity by pinging/SSHing between two EC2 instances residing in separate VPCs | 19/06/2026 | 19/06/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Achievements in Week 7:

* **AWS WAF (Web Application Firewall):**
  * Mastered how AWS WAF operates at Layer 7 (Application Layer) of the OSI model to filter and block malicious code, protecting web applications from dangerous vulnerabilities such as SQL Injection and Cross-Site Scripting (XSS).
  * Successfully configured a **Web ACL** integrated with pre-configured AWS Managed Rules and set up a Custom Rule to block specific test IP ranges. Associated this Web ACL with an Application Load Balancer to directly protect the internal web system.

* **AWS Backup:**
  * Understood the critical importance of building automated Disaster Recovery (DR) strategies to ensure high data availability for enterprises, moving away from executing manual, single snapshot creation.
  * Successfully established an automated **Backup Plan** that runs daily, securely saving backups into a dedicated **Backup Vault**. Additionally, configured a lifecycle policy to automatically transition older backups to Cold Storage after 30 days to optimize overall storage costs.

* **VPC Peering & AWS Transit Gateway (TGW):**
  * Acquired a clear understanding of network routing logic within AWS. Mastered the non-transitive nature of VPC Peering connections and learned how to resolve large-scale network management challenges using Transit Gateway as a centralized cloud router.


  * Successfully established a network connection between two separate VPCs using **VPC Peering**. After updating the respective Subnet Route Tables and adjusting Security Groups accordingly, the EC2 instances in different network segments were able to communicate directly using private IP addresses securely without routing traffic over the public Internet.