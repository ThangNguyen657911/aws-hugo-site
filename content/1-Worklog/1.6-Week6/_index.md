---
title: "Worklog Week 6"
date: 2026-06-01
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy it word-for-word** for your report, including this warning.
{{% /notice %}}


### Objectives for Week 6:

* Learn about and deploy a centralized access management solution using AWS IAM Identity Center (AWS SSO).
* Study advanced privilege control mechanisms by applying IAM Permissions Boundaries to limit the scope of permissions for IAM Entities.
* Understand secure data encryption solutions with AWS Key Management Service (KMS) and build a proactive security monitoring system using AWS Security Hub.

### Tasks to be Deployed This Week:
| Day | Task | Start Date | Completion Date | Reference Resource |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| Mon | - **AWS IAM Identity Center (AWS SSO):** <br>&emsp; + Research the theory of Single Sign-On (SSO) and the benefits of centralized identity management <br>&emsp; + Compare traditional IAM architecture with AWS IAM Identity Center | 07/06/2026 | 07/06/2026      | <https://docs.aws.amazon.com/> |
| Tue | - **AWS IAM Identity Center Practice:** <br>&emsp; + Enable the IAM Identity Center service in the active working Region <br>&emsp; + Create an administrative user group via the Identity Center Portal for secure system login | 08/06/2026 | 08/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| Wed | - **AWS IAM Permissions Boundary:** <br>&emsp; + Study the concept of Permissions Boundaries <br>&emsp; + Learn how to combine standard policies and Permissions Boundaries to establish the maximum safe limits (*Effective Permissions*) | 09/06/2026 | 09/06/2026      | <https://docs.aws.amazon.com/> |
| Thu | - **Permissions Boundary & AWS KMS Practice:** <br>&emsp; + Configure a Permissions Boundary for an IAM User, testing with excessive permissions to verify the block mechanism <br>&emsp; + Research AWS KMS, create a Customer Managed Key (CMK), and perform basic encryption/decryption | 10/06/2026 | 10/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| Fri | - **AWS Security Hub:** <br>&emsp; + Learn how Security Hub collects and aggregates security findings from multiple AWS services <br>&emsp; + Study major security standards like AWS Foundational Security Best Practices and CIS AWS Foundations Benchmark |11/06/2026 | 11/06/2026      | <https://docs.aws.amazon.com/> |
| Sat | - **AWS Security Hub Practice:** <br>&emsp; + Enable AWS Security Hub on the AWS Management Console <br>&emsp; + Read and analyze security scores, and learn how to remediate basic security vulnerabilities flagged by the system | 12/06/2026 | 12/06/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Achievements in Week 6:

* **AWS IAM Identity Center (AWS SSO):**
  * Gained a solid understanding of multi-account access architecture and centralized identity federation, which significantly reduces the risk of credential exposure.
  * Successfully enabled and configured **AWS IAM Identity Center**, setting up a dedicated Identity Portal and administrative identities for daily management tasks, completely replacing traditional IAM Users.

* **AWS IAM Permissions Boundary:**
  * Mastered the complex Policy Evaluation Logic of AWS when a Permissions Boundary is applied.
  * Successfully applied a **Permissions Boundary** to limit the maximum authority of a Developer IAM User. Even though this User was assigned a high-level policy (`AdministratorAccess`), they were effectively prevented from performing destructive actions or accessing deep system resources outside the designated boundary.

* **AWS Key Management Service (KMS):**
  * Understood the underlying principles of Symmetric and Asymmetric Encryption within cloud environments.
  * Clearly distinguished between AWS Managed Keys and Customer Managed Keys (CMKs). Successfully created a CMK, configured its Key Policy to delegate usage rights, and utilized it to test basic file encryption and decryption processes.

* **AWS Security Hub:**
  * Comprehended the role of Security Hub as a Cloud Security Posture Management (CSPM) tool that aggregates security findings from various services like Amazon GuardDuty, Amazon Inspector, and AWS IAM.
  * Successfully enabled **AWS Security Hub** and applied the *AWS Foundational Security Best Practices* standard. Based on the generated findings, analyzed and took the first steps to remediate outstanding security risks on the account (e.g., revoking unused Access Keys and hardening Security Group rules that exposed sensitive ports to the public Internet).