---
title: "Database Instance Initialization"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.6.2 </b> "
---
### 5.6.2 Database Instance Initialization

#### Implementation Steps:

1. Go to **RDS**, select **Subnet groups** and create a group named `resumematching-dbsubnetgroup` pointing to the VPC and grouping `Private-DB-A` and `Private-DB-B`.
   ![DB Subnet Group](/img/Tao_DB_Subnet_Group.jpg)
2. Initialize the Database (DB identifier: `resume-matching-db`) with **PostgreSQL** engine and database instance class `db.t3.micro`.
   ![Create RDS DB](/img/Tao_RDS_database.jpg)
3. After successful deployment, copy the Database Endpoint and update the `HOST` value in Secrets Manager.
   ![Update Secret Host](/img/Cap_nhat_Secrets_manager.jpg)
