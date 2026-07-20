---
title: "Clean Up Resources and Cost Analysis"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---
### 5.11. Clean Up Resources and Cost Analysis

---

#### 1. AWS Resource Cleanup Procedure

To avoid unnecessary costs from idle AWS resources after finishing the lab and testing, perform the following cleanup steps in order:

1. **Auto Scaling Group**: Delete the Auto Scaling Group first to prevent it from launching new instances. Terminate any remaining EC2 instances manually.
2. **Application Load Balancer (ALB)**: Delete the ALB and associated Target Groups.
3. **Database (RDS)**: Delete the PostgreSQL Database instance (skip the final snapshot option if you do not need to preserve database files). Delete the DB Subnet Group afterward.
4. **NAT Gateways**: Delete the NAT Gateways. Wait until their state is fully `Deleted`, then release allocated static Elastic IPs.
5. **VPC Infrastructure**: Clean up VPC Endpoints, Route Tables, Internet Gateway, Subnets, and finally delete the VPC `ResumeMatching-VPC`.
6. **S3 Storage**: Empty the S3 bucket `resume-matching-storage-...` and then delete the bucket.
7. **Secrets & IAM Roles**: Delete secrets from Secrets Manager and remove associated IAM Roles/Policies if no longer required.

---

#### 2. Detailed AWS Cost Breakdown Report

This report is authored from an **AWS Cloud Solutions Architect** perspective using official **AWS Pricing Calculator** figures to estimate the monthly cost of running the deployed Resume Fit 3-Tier architecture.

##### 2.1. Calculation Parameters & Assumptions
* **Deployment Region:** US East (N. Virginia) – `us-east-1`.
* **Pricing Model:** AWS On-Demand Pricing (No Reserved Instances or Savings Plans applied).
* **Operating Schedule:** 730 hours/month (24/7 continuous operation).
* **Workload Profile:** Demonstration & academic thesis defense environment (Low traffic volume).

##### 2.2. Estimated Monthly Cost Breakdown Table

| STT | AWS Service | Configuration | Quantity | Estimated Monthly Cost (USD) | Notes | Total (USD) |
| :---: | :--- | :--- | :---: | :---: | :--- | :---: |
| 1 | **Amazon VPC** | Isolated Virtual Private Cloud (`10.0.0.0/16`) | 1 | 0.00 | Core network management, free of charge | **0.000** |
| 2 | **Internet Gateway (IGW)** | Public Internet gateway for VPC | 1 | 0.00 | VPC routing component, free of charge | **0.000** |
| 3 | **Subnets** | 02 Public, 02 Private App, 02 Private DB Subnets | 6 | 0.00 | Internal network segmentation, free | **0.000** |
| 4 | **Security Groups** | Stateful Virtual Firewalls (`ALB`, `App`, `DB`, `Worker`) | 4 | 0.00 | Port & IP firewall rules, free of charge | **0.000** |
| 5 | **NAT Gateway** | Managed NAT (`us-east-1`) + 02 Public IPv4 EIPs ($0.005/h/IP) | 2 | 73.045 | $0.045/h x 2 NAT + $0.005/h x 2 EIP x 730h | **73.045** |
| 6 | **Amazon EC2** | `t3.micro` Linux (2 vCPU, 1 GiB RAM), On-Demand | 3 | 22.776 | 01 Backend + 02 ASG Instances ($0.0104/h) | **22.776** |
| 7 | **Amazon EBS Storage** | General Purpose SSD (`gp3`), 30 GB / Volume | 3 | 7.200 | 90 GB Total x $0.08/GB-month (3000 IOPS free) | **7.200** |
| 8 | **Amazon AMI** | Custom Amazon Machine Image for Backend | 1 | 0.00 | Application image storage (Free Tier) | **0.000** |
| 9 | **Launch Template** | EC2 launch configuration template for ASG | 1 | 0.00 | EC2 deployment configuration tool, free | **0.000** |
| 10 | **Auto Scaling Group** | Dynamic EC2 scaling (Desired: 2, Min: 2, Max: 4) | 1 | 0.00 | Compute auto-orchestration service, free | **0.000** |
| 11 | **Application Load Balancer** | ALB Internet-facing (`us-east-1`) + 1 LCU min traffic | 1 | 22.265 | $0.0225/h ALB + $0.008/h LCU x 730h | **22.265** |
| 12 | **Target Group** | Target Group performing Health Checks on port `8080` | 1 | 0.00 | ALB traffic routing configuration, free | **0.000** |
| 13 | **Amazon RDS PostgreSQL** | `db.t3.micro` Single-AZ + 20 GB `gp3` Storage | 1 | 15.440 | DB Instance ($13.14) + Storage ($2.30) | **15.440** |
| 14 | **Amazon S3 Standard** | Standard Tier Object Storage for CV/JD (`us-east-1`) | 5 GB | 0.120 | $0.023/GB x 5 GB + Low API Request volume | **0.120** |
| 15 | **Amazon SQS** | Standard Queue + Dead Letter Queue (DLQ) | 2 | 0.000 | Within AWS Free Tier (1M reqs/month) | **0.000** |
| 16 | **AWS Secrets Manager** | Secure storage for DB credentials & OpenAI API Key | 1 Secret | 0.400 | Management fee $0.40/secret/month | **0.400** |
| 17 | **Amazon Cognito** | User Authentication & Management (User Pool) | 1 Pool | 0.000 | Within AWS Free Tier (< 50,000 MAU) | **0.000** |
| 18 | **AWS Systems Manager** | Session Manager (Secure SSH access without Bastion) | 1 | 0.000 | Secure EC2 management access, free | **0.000** |
| 19 | **Amazon CloudWatch** | Basic Metrics (EC2/ALB) + Basic Logs (< 5 GB) | 1 | 0.500 | System performance metrics & basic logs | **0.500** |
| **TOTAL** | | | | | **ESTIMATED MONTHLY COST** | **141.746 USD** |

---

##### 2.3. Total Monthly Implementation Cost
* **Total Estimated Cost:** **$141.746 USD / month**.

##### 2.4. Cost Component Analysis
* **NAT Gateway ($73.045 USD – 51.53% of total cost):** Represents the single largest cost component.
  * *Drivers:* Maintaining 02 NAT Gateways across Availability Zones (Public Subnets A & B) for High Availability (HA) to enable private EC2 instances to reach OpenAI APIs and repository updates. Costs are driven by fixed hourly charges ($0.045/h/gateway) and public IPv4 address fees ($0.005/h/IP).
* **Amazon EC2 ($22.776 USD – 16.07%):** On-Demand cost for 3 `t3.micro` Linux instances running 24/7.
* **Application Load Balancer ($22.265 USD – 15.71%):** Fixed hourly cost ($0.0225/h) plus baseline 1 LCU usage.
* **Amazon RDS PostgreSQL ($15.440 USD – 10.89%):** Single-AZ `db.t3.micro` database instance and 20 GB `gp3` storage.
* *Remaining Services (EBS, S3, Secrets Manager, CloudWatch):* Account for only **5.80%** of total costs.

##### 2.5. AWS $200 Credits Feasibility Evaluation
* **Conclusion:** The **$200 AWS Credits** allocation is **SUFFICIENT** to cover the entire deployment and operational cost for the project evaluation period.
* **Evaluation Basis:**
  1. *Continuous 24/7 Monthly Operation:* Running 730 hours continuously for a full month costs **$141.75 USD**, leaving a buffer of **$58.25 USD** in credits.
  2. *Typical Thesis Defense Window (1–2 Weeks):* Operating the infrastructure solely during the evaluation period (7 to 14 days) costs between **$33.00 USD and $66.00 USD**, consuming less than **33%** of the allocated $200 Credits.

##### 2.6. Cost Optimization Recommendations (Architecture Retained)
To optimize costs **without altering the current 3-Tier architecture**, the following strategies are recommended:
1. **Consolidate NAT Gateways (Save $36.53/month):**
   * *Action:* Consolidate from 02 NAT Gateways down to **01 NAT Gateway** in Public Subnet A while retaining all 6 subnets. Route outbound traffic from both Private App Subnets through this single NAT Gateway.
   * *Impact:* Reduces NAT Gateway cost by 50% from $73.05 to **$36.52 USD/month**.
2. **Automated Scheduled Start/Stop:**
   * *Action:* Schedule EC2 instances to stop and set Auto Scaling Desired Capacity to `0` outside working/testing hours.
   * *Impact:* Cuts EC2 compute and ALB LCU expenses by 60–70%.
3. **Deploy S3 Gateway Endpoint (Free):**
   * *Action:* Attach a free VPC S3 Gateway Endpoint.
   * *Impact:* Routes S3 upload/download traffic over the internal AWS network, bypassing NAT Gateway data processing fees entirely.
4. **Configure CloudWatch Log Retention:**
   * *Action:* Set log retention period to **7 days** instead of *Never Expire*.
   * *Impact:* Prevents unnecessary long-term log storage accumulation.
