---
title: "IAM Permissions &  Infrastructure Setup "
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

### Introduction to VPC Endpoints in the ROMP System

A VPC Endpoint is a logically isolated, horizontally scalable, highly available virtual networking component that enables secure communication between your workloads and supported AWS services without exposing traffic to the public Internet.

Within the **Retail Operations Monitoring Platform (ROMP)** architecture, protecting data in transit is a critical requirement.

* **Gateway Endpoint:** Used by AWS Lambda functions inside the VPC to securely read and write data directly to Amazon DynamoDB using private IP addresses.

* **Interface Endpoint (AWS PrivateLink):** Used to establish private connectivity to other AWS services (such as Amazon SES or Amazon CloudWatch) or to provide secure communication between the cloud monitoring layer and the enterprise on-premises infrastructure.

---

### Workshop Environment Overview

To simulate a real enterprise environment, this workshop uses a hybrid network architecture consisting of two environments:

1. **ROMP Cloud VPC**

   This environment hosts the serverless monitoring components, including the following AWS Lambda functions:

   * Inventory Monitoring
   * Expiry Monitoring
   * Promotion Monitoring
   * Sales Monitoring

   These Lambda functions are deployed inside **Private Subnets** and use dedicated IAM Roles to securely access AWS resources.

2. **On-Premises Network VPC**

   This environment simulates the organization's traditional data center where the core **Oracle Database** is deployed.

---

## Deployment

#### IAM Role

![overview](/images/5-Workshop/5.1-Workshop-overview/IAM1.jpg)

* In the search bar at the top of the AWS Console, type **IAM** and open the **IAM** service.

* From the left navigation menu, select **Roles**.

* Click **Create role**.

---

![overview](/images/5-Workshop/5.1-Workshop-overview/IAM2.jpg)

Configure the trusted entity:

* Under **Select trusted entity type**, choose **AWS service**.

* Under **Use case**, select **Lambda** from the dropdown list.

* Click **Next**.

---

![overview](/images/5-Workshop/5.1-Workshop-overview/IAM3.jpg)

Under **Permission policies**:

* In the search box, search for:

```
AWSLambdaBasicExecutionRole
```

* Select the policy by checking the corresponding checkbox.

---

![overview](/images/5-Workshop/5.1-Workshop-overview/IAM4.jpg)

* Search for the following policy:

```
AWSLambdaVPCAccessExecutionRole
```

* Select the policy.

* Click **Next**.

---

![overview](/images/5-Workshop/5.1-Workshop-overview/IAM5.jpg)

Configure the role details:

* **Role name**

```
ROMP-Lambda-ExecutionRole
```

* **Description**

```
Shared execution role for ROMP Lambda functions (Inventory, Expiry, Promotion, Sales).
```

* Scroll down and review the **Trusted entities** and **Permissions**.

* Click **Create role**.

---

![overview](/images/5-Workshop/5.1-Workshop-overview/IAM6.jpg)

After the role has been created:

* You will be redirected to the newly created role page.

Alternatively, navigate to:

```
Roles
→ ROMP-Lambda-ExecutionRole
```

* Open the **Permissions** tab.

* Click:

```
Add permissions
→ Create inline policy
```

---

![overview](/images/5-Workshop/5.1-Workshop-overview/IAM7.jpg)

Select the **JSON** tab and paste the following policy:

```properties
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ROMPDynamoDBAccess",
      "Effect": "Allow",
      "Action": [
        "dynamodb:PutItem",
        "dynamodb:GetItem",
        "dynamodb:UpdateItem",
        "dynamodb:Query"
      ],
      "Resource": "arn:aws:dynamodb:AP_SOUTHEAST_1:ACCOUNT_ID:table/ROMP-AlertHistory"
    }
  ]
}
```

---

![overview](/images/5-Workshop/5.1-Workshop-overview/IAM8.jpg)

* Click **Next**.

* **Policy name**

```
ROMP-DynamoDB
```

* Click **Create policy**.

---

![overview](/images/5-Workshop/5.1-Workshop-overview/IAM9.jpg)

Create another inline policy:

```
Add permissions
→ Create inline policy
→ JSON
```

Paste the following policy:

```properties
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ROMPSESSendEmail",
      "Effect": "Allow",
      "Action": [
        "ses:SendEmail",
        "ses:SendRawEmail"
      ],
      "Resource": "*"
    }
  ]
}
```

---

![overview](/images/5-Workshop/5.1-Workshop-overview/IAM10.jpg)

Configure the policy name:

```
ROMP-SES
```

Click **Create policy**.

### Create the VPC

![overview](/images/5-Workshop/5.1-Workshop-overview/VPC1.jpg)

* Open the **VPC Dashboard** in the AWS Console.

* Click **Create VPC**.

---

![overview](/images/5-Workshop/5.1-Workshop-overview/VPC2.jpg)

* Under **Resources to create**, choose **VPC and more**.

---

![overview](/images/5-Workshop/5.1-Workshop-overview/VPC3.jpg)

Configure the following settings:

* **Name tag auto-generation:** `ROMP-VPC`

* **IPv4 CIDR block:** `10.0.0.0/16`

---

![overview](/images/5-Workshop/5.1-Workshop-overview/VPC4.jpg)

Configure the network layout:

* **Number of Availability Zones (AZs):** `1`
  (To reduce cost and match the workshop architecture. Select any AZ, for example `ap-southeast-1a`.)

* **Number of Public Subnets:** `1`

* Change the Public Subnet CIDR block to:

```
10.0.1.0/24
```

* **Number of Private Subnets:** `1`

* Change the Private Subnet CIDR block to:

```
10.0.2.0/24
```

---

![overview](/images/5-Workshop/5.1-Workshop-overview/VPC5.jpg)

Configure the remaining options:

* **NAT Gateways:** Select **1 per AZ**

  AWS will automatically create one NAT Gateway inside the Public Subnet.

* **VPC Endpoints:** Select **None**

  (Not required for this workshop and avoids additional charges.)

Finally, click **Create VPC** and wait several minutes while AWS provisions the networking resources.

---

## Create the Lambda Security Group

Since the EC2 Oracle server must explicitly allow traffic from Lambda, create the Lambda Security Group first.

![overview](/images/5-Workshop/5.1-Workshop-overview/SG1.jpg)

* Open the **EC2 Dashboard**.

* Navigate to:

```
Security Groups
```

* Click **Create security group**.

---

![overview](/images/5-Workshop/5.1-Workshop-overview/SG2.jpg)

Configure the Security Group:

* **Security group name**

```
ROMP-Lambda-SG
```

* **Description**

Example:

```
Security Group for Lambda functions
```

* **VPC**

Select your workshop VPC:

```
ROMP-VPC
```

---

![overview](/images/5-Workshop/5.1-Workshop-overview/SG3.jpg)

Click **Create security group**.

After the Security Group is created, copy and save its **Security Group ID (sg-xxxxxxx)** because it will be used later.

---

## Create the Oracle EC2 Security Group

![overview](/images/5-Workshop/5.1-Workshop-overview/SG1.jpg)

Click **Create security group** again.

---

![overview](/images/5-Workshop/5.1-Workshop-overview/SG4.jpg)

Configure the Security Group:

* **Security group name**

```
ROMP-Oracle-SG
```

* **Description**

Example:

```
Security Group for Oracle EC2 Database
```

* **VPC**

Select:

```
ROMP-VPC
```

---

![overview](/images/5-Workshop/5.1-Workshop-overview/SG5.jpg)

### Configure Inbound Rules

Click **Add rule** and create the following two inbound rules.

### Rule 1 — Allow Lambda to Connect to Oracle Database

* **Type**

```
Custom TCP
```

* **Port range**

```
1521
```

* **Source**

Choose **Custom** and select (or paste) the Security Group ID of **ROMP-Lambda-SG**.

---

### Rule 2 — Allow SSH Access from Your Computer

* **Type**

```
SSH
```

* **Port**

```
22
```

* **Source**

Choose:

```
My IP
```

Finally, click **Create security group**.

---

![overview](/images/5-Workshop/5.1-Workshop-overview/SG6.jpg)

Completed Security Group configuration.

---

## Attach the Security Groups

After creating both Security Groups, attach them to the corresponding resources.

### Lambda

Navigate to:

```
Lambda
→ Configuration
→ VPC
→ Edit
```

Select:

```
ROMP-Lambda-SG
```

---

### Oracle EC2

Navigate to:

```
EC2
→ Select Oracle Instance
→ Actions
→ Security
→ Change Security Groups
```

Select:

```
ROMP-Oracle-SG
```

Remove the default Security Groups if necessary.

---

## Launch the EC2 Instance

![overview](/images/5-Workshop/5.1-Workshop-overview/EC21.jpg)

Open the **EC2 Dashboard** and click **Launch instance**.

---

![overview](/images/5-Workshop/5.1-Workshop-overview/EC22.jpg)

Configure:

**Name**

```
ROMP-Oracle-Server
```

**Application and OS Images**

Choose:

```
Ubuntu
```

---

![overview](/images/5-Workshop/5.1-Workshop-overview/EC23.jpg)

Configure:

**Amazon Machine Image**

Choose either:

* Ubuntu Server 24.04 LTS
* Ubuntu Server 22.04 LTS

Both are Free Tier eligible.

**Instance Type**

```
t3.small
```

---

![overview](/images/5-Workshop/5.1-Workshop-overview/EC24.jpg)

Edit the network settings:

* **VPC**

```
ROMP-VPC
```

* **Subnet**

```
Private Subnet (10.0.2.0/24)
```

* **Auto-assign Public IP**

```
Disable
```

* **Firewall**

Select the existing Security Group:

```
ROMP-Oracle-SG
```

Click **Launch instance** and wait until the instance is running.

---

# Connect to EC2 via SSH

After launching the EC2 instance:

* Download the **.pem** key pair.

* Create a folder named:

```
keys
```

* Place the `.pem` file inside the folder.

Then connect using:

```bash
ssh -i .\ROMP-Oracle-Key.pem ubuntu@<EC2-IP>
```

The successful connection should look similar to the following.

![overview](/images/5-Workshop/5.1-Workshop-overview/SSH1.jpg)

---

# Update Ubuntu and Install Required Packages

### Step 1. Update Ubuntu

```bash
sudo apt-get update && sudo apt-get upgrade -y
```

---

### Step 2. Install Oracle Dependencies

```bash
sudo apt-get install -y alien libaio1 unixodbc dnsutils network-manager
```

---

### Step 3. Create a Temporary Directory

```bash
mkdir ~/oracle21c
cd ~/oracle21c
```

![overview](/images/5-Workshop/5.1-Workshop-overview/SSH2.jpg)

![overview](/images/5-Workshop/5.1-Workshop-overview/SSH3.jpg)

---

### Step 4. Download Oracle Database XE 21c

The RPM package is approximately **2 GB**.

```bash
wget https://download.oracle.com/otn-pub/otn_software/db-express/oracle-database-xe-21c-1.0-1.x86_64.rpm
```

---

### Step 5. Convert RPM to DEB

> **Note**
>
> This process may take **10–15 minutes**.
> During conversion, the terminal may appear to be frozen. Please wait until the command completes.

```bash
sudo alien --to-deb --scripts oracle-database-xe-21c-1.0-1.x86_64.rpm
```

---

### Step 6. Install Oracle XE

```bash
sudo dpkg -i oracle-database-xe-21c_*.deb
```

---

### Step 7. Configure Oracle Database

```bash
sudo /etc/init.d/oracle-xe-21c configure
```

---

### Start Oracle Service

```bash
sudo systemctl start oracle-xe-21c
```

Enable Oracle to start automatically after reboot.

```bash
sudo systemctl enable oracle-xe-21c
```

Verify the service status.

```bash
sudo systemctl status oracle-xe-21c
```

Ensure the status shows:

```
active (running)
```

---

# Oracle Deployment Using Docker

```properties
Step 1. Pull the Oracle XE Image

docker pull gvenzl/oracle-xe:21-slim



Step 2. Verify the Image

docker images



Step 3. Create a Persistent Data Directory

mkdir -p ~/oracle-data



Step 4. Run Oracle XE

docker run -d \
--name oracle-xe \
-p 1521:1521 \
-p 5500:5500 \
-e ORACLE_PASSWORD=123456 \
-v ~/oracle-data:/opt/oracle/oradata \
gvenzl/oracle-xe:21-slim



Step 5. Verify the Container

docker ps


Step 6. Monitor the Container Logs

docker logs -f oracle-xe
```

After completing these steps, Oracle Database XE is successfully deployed on the EC2 instance and ready for use.