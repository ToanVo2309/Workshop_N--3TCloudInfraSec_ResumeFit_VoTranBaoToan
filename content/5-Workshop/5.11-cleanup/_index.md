---
title: "Clean Up Resources"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---
### 5.11. Clean Up Resources and Cost Estimation

#### 1. Resource Cleanup Procedure

To avoid unnecessary costs from idle AWS resources after completing the lab and testing, perform the cleanup steps in the following order:

1. **Auto Scaling Group**: Delete the Auto Scaling Group first to prevent it from automatically spawning new instances. Terminate remaining EC2 instances manually.
2. **Application Load Balancer (ALB)**: Delete the ALB and associated Target Groups.
3. **Database (RDS)**: Delete the PostgreSQL Database instance (skip the final snapshot option if data preservation is not required). Delete the DB Subnet Group.
4. **NAT Gateways**: Delete allocated NAT Gateways. Wait until state changes to `Deleted`, then release static Elastic IPs.
5. **VPC Infrastructure**: Clean up Route Tables, Internet Gateway, Subnets, and delete the VPC `ResumeMatching-VPC`.
6. **S3 Storage**: Empty all objects in the S3 bucket `resume-matching-storage-...` and delete the bucket.
7. **Secrets Manager & IAM**: Delete stored secrets in AWS Secrets Manager and remove associated IAM Roles/Policies.

---

#### 2. Infrastructure Cost Estimation (Cost Breakdown)

##### 2.1. Calculation Methodology & Assumptions
* **Estimation Tool:** AWS Pricing Calculator (Official AWS Pricing Reference).
* **Target Region:** US East (N. Virginia) – `us-east-1`.
* **Pricing Model:** AWS On-Demand Pricing (No Reserved Instances or Savings Plans applied).
* **Operating Schedule:** 730 hours/month (24/7 continuous operation).
* **Traffic Profile:** Low traffic profile tailored for project demonstration and grading.

##### 2.2. Detailed AWS Service Monthly Cost Breakdown

| STT | AWS Service | Configuration | Quantity | Estimated Monthly Cost (USD) | Notes | Total (USD) |
| :---: | :--- | :--- | :---: | :---: | :--- | :---: |
| **1** | **Amazon VPC** | VPC 10.0.0.0/16, 2 Public Subnets, 4 Private Subnets, Internet Gateway | 01 VPC | 0.00 | Virtual network infrastructure free of charge | **0.00** |
| **2** | **Security Group** | Virtual Firewalls (ALB-SG, Backend-SG, Worker-SG, RDS-SG) | 04 SGs | 0.00 | Inbound/Outbound security rules management | **0.00** |
| **3** | **NAT Gateway** | Managed NAT Gateway ($0.045/hour/gateway + $0.045/GB data) | 02 Gateways | 65.75 | 1,460 hours On-Demand + ~1 GB Data Processed | **65.75** |
| **4** | **Amazon EC2** | `t3.micro` Linux (2 vCPU, 1 GiB RAM), On-Demand ($0.0104/hour) | 03 Instances | 22.78 | 01 Backend Server + 02 EC2 in Auto Scaling Group | **22.78** |
| **5** | **Amazon EBS** | `gp3` General Purpose SSD Storage, 30 GB per instance | 03 Volumes (90 GB) | 7.20 | $0.08/GB-month x 90 GB total allocation | **7.20** |
| **6** | **AMI & Launch Template** | Launch Template configuration & custom Amazon Machine Image | 01 LT, 01 AMI | 0.00 | Instance template storage free of charge | **0.00** |
| **7** | **Auto Scaling Group** | Dynamic Auto Scaling Group (Min: 2, Max: 4, Desired: 2) | 01 ASG | 0.00 | Auto Scaling orchestration service free of charge | **0.00** |
| **8** | **Application Load Balancer** | Internet-facing ALB, Multi-AZ ($0.0225/hour + LCU) | 01 ALB | 16.44 | 730 hours operation + < 1 LCU traffic | **16.44** |
| **9** | **Target Group** | Instance-type Target Group (HTTP Port 8080) | 01 Target Group | 0.00 | Target routing configuration free of charge | **0.00** |
| **10** | **Amazon RDS PostgreSQL** | Single-AZ `db.t3.micro` ($0.018/hour) + 20 GB `gp3` Storage ($0.08/GB) | 01 DB Instance | 14.74 | $13.14 (Compute) + $1.60 (Storage) | **14.74** |
| **11** | **Amazon S3** | S3 Standard Storage (~5 GB CV/JD files, $0.023/GB) | 01 Bucket | 0.12 | Candidate CV & JD files object storage | **0.12** |
| **12** | **Amazon SQS & DLQ** | Standard Queue & Dead Letter Queue (< 1,000 requests/month) | 02 SQS Queues | 0.00 | Covered by AWS Free Tier (1M requests/month) | **0.00** |
| **13** | **AWS Secrets Manager** | Secret storing DB Credentials, Auth Keys & OpenAI API Key | 01 Secret | 0.40 | Fixed charge $0.40/secret/month | **0.40** |
| **14** | **Amazon Cognito** | User Pool managing user authentication (< 50,000 MAU) | 01 User Pool | 0.00 | Always free under 50,000 Monthly Active Users | **0.00** |
| **15** | **AWS Systems Manager** | Session Manager secure shell terminal access to EC2 | 01 Service | 0.00 | Administrative shell access free of charge | **0.00** |
| **16** | **Amazon CloudWatch** | Basic Metrics (5-min frequency) + Basic Monitoring Logs | 01 Dashboard | 0.00 | Covered under standard monitoring tier | **0.00** |
| **TOTAL** | | | | | | **127.43 USD** |

##### 2.3. Cost Breakdown & Infrastructure Analysis

1. **Total Monthly Operating Cost:**
   * Total estimated monthly cost to maintain the Resume Fit system is **$127.43 USD / month**.

2. **Cost Distribution Analysis:**
   * **Highest Cost Driver:** **NAT Gateway** incurring **$65.75 USD / month** (**51.6%** of total budget). Fixed hourly charges for dual NAT Gateways ($0.045/hour x 2) represent the dominant cost component.
   * **Compute Tier (EC2 & EBS):** Combined cost for 3 `t3.micro` instances and 90 GB `gp3` storage is **$29.98 USD / month** (**23.5%**).
   * **Load Balancing (ALB):** ALB fixed availability fee is **$16.44 USD / month** (**12.9%**).
   * **Database Tier (RDS PostgreSQL):** Single-AZ `db.t3.micro` instance fee is **$14.74 USD / month** (**11.6%**).

3. **Evaluation against $200 USD AWS Credit Limit:**
   * A **$200 USD AWS Credit** budget is **FULLY SUFFICIENT** to run the complete production environment 24/7 for **1.5 months (approx. 47 days)**.
   * Under realistic demo conditions (operating ~8-10 hours/day during evaluation), the $200 credit easily extends operational lifespan to **3 to 4 months**.

##### 2.4. Cost Optimization Recommendations
Cost reduction strategies while preserving the current 3-Tier architecture:

* **Consolidate NAT Gateways in Dev/Test:** Consolidate from 2 NAT Gateways down to 1 NAT Gateway in `Public Subnet A` (routing `Private Subnet B` traffic through NAT Gateway A). Saves **$32.88 USD / month** immediately with zero application logic impact.
* **Automated Operational Schedules (Auto Stop/Start):** Implement AWS EventBridge schedules to automatically stop EC2 and RDS instances during non-working hours, reducing compute costs by up to 60% (saving **~$25.00 USD / month**).
* **CloudWatch Log Retention Policies:** Set CloudWatch log retention to 7 days instead of `Never Expire` to prevent accumulating log storage costs.
