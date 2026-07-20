---
title: "Clean Up Resources"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---
### 5.11. Clean Up Resources & Cost Breakdown

#### 1. Resource Cleanup Procedure

To avoid unnecessary costs from idle AWS resources after lab execution and testing, perform the following cleanup steps in order:

1. **Auto Scaling Group**: Delete the Auto Scaling Group first to prevent it from automatically launching new EC2 instances. Terminate any remaining instances.
2. **Application Load Balancer (ALB)**: Delete the ALB and associated Target Groups.
3. **Database (RDS)**: Delete the PostgreSQL Database instance (skip the final snapshot option if you do not need to preserve database files). Delete the DB Subnet Group afterward.
4. **NAT Gateways**: Delete the NAT Gateways. Wait until their state is fully `Deleted`, then release allocated static Elastic IPs.
5. **VPC Infrastructure**: Clean up VPC Endpoints, Route Tables, Internet Gateway, Subnets, and finally delete the VPC `ResumeMatching-VPC`.
6. **S3 Storage**: Empty the S3 bucket `resume-matching-storage-...` and then delete the bucket.
7. **Secrets & IAM Roles**: Delete secrets from Secrets Manager and remove associated IAM Roles/Policies.

---

#### 2. Cost Analysis Report (AWS Cost Breakdown)

This cost estimation report for the **Resume Fit** platform is compiled by an **AWS Cloud Solutions Architect** using official calculation metrics from the **AWS Pricing Calculator**.

##### 2.1. Assumptions and Parameters
* **Deployment Region:** US East (N. Virginia) – `us-east-1`.
* **Pricing Model:** AWS On-Demand Pricing (No Reserved Instances or Savings Plans applied).
* **Operating Duration:** 730 hours/month (24/7 continuous operation).
* **Traffic Load:** Low traffic volume intended for academic project demonstration and evaluation.

##### 2.2. Detailed Monthly Cost Estimation Table

| No. | AWS Service | Configuration | Quantity | Estimated Monthly Cost (USD) | Notes | Total (USD) |
| :---: | :--- | :--- | :---: | :---: | :--- | :---: |
| **1** | **Amazon VPC** | Virtual Private Cloud (`10.0.0.0/16`) | 01 | 0.00 | Base virtual network, no setup fee | 0.00 |
| **2** | **Internet Gateway** | Internet Gateway (IGW) for VPC internet access | 01 | 0.00 | Free Inbound/Outbound gateway routing | 0.00 |
| **3** | **Subnets** | 2 Public, 2 Private App, 2 Private DB Subnets | 06 | 0.00 | Subnet partition configuration | 0.00 |
| **4** | **NAT Gateway** | Managed NAT Gateway ($0.045/hr + Data Processing) | 02 | 65.70 | 2 NATs x 730h x $0.045/hr (HA across 2 AZs) | 65.70 |
| **5** | **Security Group** | Virtual Firewall controlling Inbound/Outbound | 04 | 0.00 | Free firewall rules configuration | 0.00 |
| **6** | **Amazon EC2** | `t3.micro` Linux (2 vCPU, 1 GiB RAM, $0.0104/hr) | 03 | 22.78 | 01 Standalone Backend + 02 ASG Instances | 22.78 |
| **7** | **Amazon EBS Storage** | `gp3` SSD Storage (30 GB/instance, $0.08/GB/month) | 90 GB | 7.20 | OS & Backend/Worker application storage | 7.20 |
| **8** | **Amazon Machine Image** | Custom AMI (`ResumeMatching-Backend-AMI`) | 01 | 0.00 | Free AMI management (EBS charges apply) | 0.00 |
| **9** | **Launch Template & ASG** | Launch Template & Auto Scaling Group | 01 | 0.00 | Free auto scaling management service | 0.00 |
| **10** | **Application Load Balancer** | ALB ($0.0225/hr + LCU usage) | 01 | 16.88 | 730h x $0.0225/hr + LCU demo traffic | 16.88 |
| **11** | **Target Group** | Target Group routing HTTP Port 8080 | 01 | 0.00 | Health check configuration included | 0.00 |
| **12** | **Amazon RDS PostgreSQL** | Single-AZ `db.t3.micro` Instance ($0.018/hr) | 01 | 13.14 | 730h x $0.018/hr (PostgreSQL DB) | 13.14 |
| **13** | **Amazon RDS Storage** | `gp3` Database Storage (20 GB, $0.115/GB/month) | 20 GB | 2.30 | Application relational database storage | 2.30 |
| **14** | **Amazon S3 Standard** | Standard Object Storage (CV/JD, $0.023/GB/month) | 5 GB | 0.12 | 5 GB storage + basic request operations | 0.12 |
| **15** | **Amazon SQS & DLQ** | Standard Queue & Dead Letter Queue | 02 Queues | 0.00 | Covered by AWS Free Tier (1M free requests/mo) | 0.00 |
| **16** | **AWS Secrets Manager** | Sensitive Secret Storage ($0.40/secret/month) | 01 Secret | 0.40 | Manages OpenAI API Key & DB Credentials | 0.40 |
| **17** | **Amazon Cognito** | User Pool Authentication (MAU < 50,000) | 01 Pool | 0.00 | Free for first 50,000 Monthly Active Users | 0.00 |
| **18** | **AWS Systems Manager** | SSM Session Manager secure SSH access | Active | 0.00 | Free EC2 management without port 22 open | 0.00 |
| **19** | **Amazon CloudWatch** | Basic Monitoring & Log Ingestion (5 GB free) | Active | 0.00 | Free basic metrics & 5 GB log ingestion | 0.00 |
| **TOTAL** | | | | | **Total Monthly Estimated Cost** | **$128.52** |

---

##### 2.3. Total Monthly Estimated Cost
The total estimated monthly cost to operate the complete **Resume Fit** system infrastructure 24/7 (730 hours) is **$128.52 USD / month** (approximately **3,213,000 VND / month** assuming 1 USD = 25,000 VND).

##### 2.4. Cost Drivers Analysis
1. **NAT Gateway ($65.70 - 51.1% of total cost):**
   - Represents the largest cost component. Maintaining 02 NAT Gateways across 02 Availability Zones (AZ A & AZ B) for High Availability (HA) incurs a fixed hourly charge ($0.045/hr per NAT Gateway), independent of data traffic volume.
2. **Compute EC2 & EBS Storage ($29.98 - 23.3% of total cost):**
   - Running 03 `t3.micro` instances 24/7 costs $22.78/month, while 90 GB of attached `gp3` SSD storage accounts for $7.20/month.
3. **Application Load Balancer ($16.88 - 13.1% of total cost):**
   - Fixed hourly charge for maintaining ALB to distribute inbound internet traffic to private subnet EC2 instances.
4. **Amazon RDS PostgreSQL Database ($15.44 - 12.0% of total cost):**
   - Includes the `db.t3.micro` instance ($13.14/mo) and 20 GB `gp3` storage ($2.30/mo).

##### 2.5. AWS Credits Evaluation ($200 Credit Limit)
* **Conclusion:** The system cost is **FULLY COMPATIBLE** and well within the **$200 USD AWS Credit** allowance.
* **Detailed Breakdown:**
  - Running 24/7 continuous operation ($128.52/month), the $200 USD Credit covers full system operation for **1.55 months** (~46 days) with zero out-of-pocket expense.
  - In a realistic demonstration setup (running only during testing and evaluation hours, e.g., 8 hours/day, 5 days/week), operational costs drop to **~$43.00/month**, allowing the $200 Credit to sustain the project for up to **4.6 months**.

##### 2.6. Cost Optimization Recommendations
To optimize costs while **preserving the exact current architecture**, the following strategies are recommended:
1. **Single NAT Gateway for Demo Environment (Saves $32.85/month):**
   - During evaluation, consolidate to **01 NAT Gateway** shared across both Private Subnets instead of 02 NAT Gateways across 2 AZs. This cuts NAT Gateway costs by 50%, reducing total monthly cost to **$95.67/month** (a 25.5% overall savings).
2. **Scheduled Auto Start/Stop:**
   - Use AWS EventBridge and Lambda to automatically stop EC2 and RDS instances during non-evaluation hours (e.g., 10 PM to 7 AM and weekends), reducing compute costs by up to 60%.
3. **Prompt Resource Deletion:**
   - Execute the cleanup sequence in Section 5.11.1 immediately after project evaluation to prevent idle resource charges.
