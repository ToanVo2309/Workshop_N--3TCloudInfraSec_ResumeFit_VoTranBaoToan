---
title: "Week 6 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:
* Learn database virtualization with Amazon Relational Database Service (RDS).
* Secure databases inside Private Subnets and configure access authorization.
* Configure automated backup policies, manual snapshots, and restore operations.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | ---------- | --------------- | ------------------ |
| Monday | Study Amazon RDS engines (MySQL/PostgreSQL), storage classes, and Subnet Groups. | 25/05/2026 | 25/05/2026 | [Video](https://www.youtube.com/watch?v=hZ-kH52vdfg) <br> [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html) |
| Tuesday | Learn RDS reliability options: Multi-AZ deployments for failover and Read Replicas for scaling. | 26/05/2026 | 26/05/2026 | [RDS Multi-AZ Deployments](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html) |
| Wednesday | Deploy an RDS MySQL instance inside isolated private subnets and configure Subnet Groups. | 27/05/2026 | 27/05/2026 | [RDS inside VPC Subnets](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html) |
| Thursday | Configure security groups to allow database connection access ONLY from front-end EC2 instances. | 28/05/2026 | 28/05/2026 | [EC2 to RDS Connectivity](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.Scenarios.html) |
| Friday | Enable automated backups, perform a manual database Snapshot, and execute point-in-time recovery. | 29/05/2026 | 29/05/2026 | [RDS Automated Backups](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithAutomatedBackups.html) |

### Week 6 Achievements:
* Created a highly secure, network-isolated database instance matching enterprise standards.
* Established network isolation preventing database exposure to the public internet.
* Configured automatic master-standby failover parameters for disaster recovery.
* Validated backup restore pipelines ensuring business continuity in database corruption events.
