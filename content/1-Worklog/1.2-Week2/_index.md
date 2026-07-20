---
title: "Worklog Week 2"
date: 2026-05-04
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your official report, including this warning.
{{% /notice %}}


### Week 2 Objectives:

* Master the foundational knowledge and gain hands-on experience in building secure, isolated virtual networks on AWS using Amazon VPC.
* Understand, install, and configure the AWS CLI to manage system resources directly from the command-line interface instead of the AWS Console.
* Study Amazon Route 53 global DNS management and hybrid DNS resolution architectures between On-Premises environments and AWS Cloud.

### Tasks to be Deployed This Week:
| Day | Task | Start Date | Completion Date | Resource Sources |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2 | - **Amazon VPC Foundational Knowledge:** <br>&emsp; + Learn about network division models (CIDR, Subnets, Public/Private IP) <br>&emsp; + Understand routing mechanisms: Route Tables, Internet Gateway (IGW), NAT Gateway, NAT Instance | 11/05/2026   | 11/05/2026      | <https://docs.aws.amazon.com/> <br> <https://cloudjourney.awsstudygroup.com/> |
| 3 | - **Hands-on Building Basic VPC:** <br>&emsp; + Manually initialize a VPC with key components: Public Subnet, Private Subnet <br>&emsp; + Configure Route Tables and attach an Internet Gateway to allow Public Subnet Internet access <br>&emsp; + Configure Security Groups (instance-level firewall) and Network ACLs (subnet-level firewall) | 12/05/2026   | 12/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **AWS CLI (Command Line Interface):** <br>&emsp; + Overview and installation of AWS CLI on personal OS <br>&emsp; + Configure credential identification (`aws configure`) using Access Key / Secret Key of the Admin IAM User <br>&emsp; + Practice basic CLI commands to query VPC and EC2 resources | 13/05/2026   | 13/05/2026      | <https://docs.aws.amazon.com/> |
| 5 | - **Amazon Route 53:** <br>&emsp; + Learn common DNS record types (A, AAAA, CNAME, MX, TXT) <br>&emsp; + Understand Hosted Zones (Public Hosted Zone and Private Hosted Zone) <br>&emsp; + Explore DNS Routing Policies: Simple, Weighted, Latency, Failover, Geolocation, Multi-value answer | 14/05/2026   | 14/05/2026      | <https://docs.aws.amazon.com/> |
| 6 | - **Hybrid DNS & Route 53 Resolver:** <br>&emsp; + Understand challenges of resolving domain names between self-managed enterprise infrastructures (On-Premises) and AWS Cloud <br>&emsp; + Study the mechanics of Route 53 Resolver Inbound Endpoints, Outbound Endpoints, and Resolver Rules | 15/05/2026   | 15/05/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 7 | - **Hands-on Route 53 & Hybrid DNS:** <br>&emsp; + Configure a Private Hosted Zone associated with a VPC <br>&emsp; + Simulate a hybrid DNS resolution scenario by setting up Route 53 Resolver Rules and Endpoints directed to a self-hosted DNS Server <br>&emsp; + Test and verify successful bi-directional domain resolution | 16/05/2026   | 16/05/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Achievements in Week 2:

* **Amazon VPC:**
  * Acquired a deep understanding of how AWS isolates customer network resources. Clearly distinguished the roles of **Public Subnets** (for external-facing services requiring direct internet communication like Web Servers) and **Private Subnets** (for backends and databases demanding high security).
  * Mastered the operational mechanics of **NAT Gateways** in enabling resources in Private Subnets to connect outbound to the Internet for updates while blocking unsolicited inbound connections.
  * Differentiated between two network security layers: **Security Groups** (Stateful - automatically tracking connection states) and **Network ACLs** (Stateless - requiring explicit inbound and outbound rule configurations).

* **AWS CLI:**
  * Successfully installed AWS CLI on a personal machine and configured secure programmatic access using a dedicated profile powered by the IAM Access Key / Secret Key generated in Week 1.
  * Achieved proficiency in executing essential CLI commands to manage and query resources efficiently without the console GUI (e.g., `aws ec2 describe-vpcs`, `aws s3 ls`), paving the way for future task automation.

* **Amazon Route 53:**
  * Mastered DNS management concepts, successfully configuring **Public Hosted Zones** (for internet-facing domain resolution) and **Private Hosted Zones** (strictly for internal resolution restricted within specified VPCs).
  * Understood how to apply flexible Routing Policies tailored to real-world scenarios (such as routing traffic based on lowest latency to users, or configuring automatic failover to a standby server in case of primary server downtime).

* **Hybrid DNS & Route 53 Resolver:**
  * Solved the critical challenge of bridging DNS environments between AWS Cloud and legacy On-Premises infrastructures using **Route 53 Resolver**.
  * Thoroughly understood the mechanics: **Inbound Endpoints** allow On-Premises DNS servers to query private domain records inside AWS Private Hosted Zones; conversely, **Outbound Endpoints** combined with **Resolver Rules** forward internal corporate DNS queries from AWS back to On-Premises DNS systems.
  * Successfully conducted hands-on verification and troubleshooting of bi-directional hybrid domain queries, ensuring local corporate domain lookups remain highly secure and never leak into the public internet.