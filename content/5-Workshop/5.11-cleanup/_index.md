---
title: "Clean Up Resources"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---
### 5.11. Clean Up Resources

To avoid unnecessary costs from idle AWS resources, perform the following cleanup steps in order:

1. **Auto Scaling Group**: Delete the Auto Scaling Group first to prevent it from launching new instances. Terminate any remaining EC2 instances.
2. **Application Load Balancer (ALB)**: Delete the ALB and associated Target Groups.
3. **Database (RDS)**: Delete the PostgreSQL Database instance (skip the final snapshot option if you do not need to preserve database files). Delete the DB Subnet Group afterward.
4. **NAT Gateways**: Delete the NAT Gateways. Wait until their state is fully `Deleted`, then release allocated Elastic IPs.
5. **VPC Infrastructure**: Clean up VPC Endpoints, Route Tables, Internet Gateway, Subnets, and finally delete the VPC `ResumeMatching-VPC`.
6. **S3 Storage**: Empty the S3 bucket `resume-matching-storage-...` and then delete the bucket.
7. **Secrets & IAM Roles**: Delete secrets from Secrets Manager and remove associated IAM Roles/Policies if no longer required.
