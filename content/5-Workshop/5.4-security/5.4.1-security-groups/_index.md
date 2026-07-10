---
title: "Security Groups Creation"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.4.1 </b> "
---
### 5.4.1 Security Groups Creation

Configure virtual firewalls to control traffic between resources.

#### Implementation Steps:

1. **ALB Security Group** (`ResumeMatching-ALB-SG`): Open HTTP (`80`) and HTTPS (`443`) ports (TCP) from source `0.0.0.0/0` to allow user web access.
   ![ALB Security Group](/img/Tao_ALB_Security_Group.jpg)
2. **Backend Security Group** (`ResumeMatching-Backend-SG`): Configure an Inbound rule allowing HTTP traffic on port `8080`. The Source is restricted to `ResumeMatching-ALB-SG`.
   ![Backend Security Group](/img/Tao_Backend_Security_Group.jpg)
3. **Worker Security Group** (`ResumeMatching-Worker-SG`): Security group protecting Worker Servers processing background jobs.
   ![Worker Security Group](/img/T%E1%BA%A1o_Worker_Security_Group.jpg)
4. **Database Security Group** (`ResumeMatching-RDS-SG`): Open port `5432` (PostgreSQL). The Source is restricted to traffic from Backend and Worker Security Groups.
   ![Database Security Group](/img/Tao_Database_Security_Group.jpg)
