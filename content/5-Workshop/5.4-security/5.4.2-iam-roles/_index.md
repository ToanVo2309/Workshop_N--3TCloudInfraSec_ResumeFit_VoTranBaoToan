---
title: "IAM Roles Configuration"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.4.2 </b> "
---
### 5.4.2 IAM Roles Configuration

Authorize EC2 instances to communicate securely with other AWS services without hard-coding access credentials.

#### Implementation Steps:

1. Go to **IAM**, create a role named `ResumeMatching-Backend-Role` for the backend servers running on EC2.
   ![Backend IAM Role](/img/Tao_Backend_IAM_Role.jpg)
2. Create a second role named `ResumeMatching-Worker-Role` dedicated to the Worker server. Attach managed policies like `AmazonSQSFullAccess` and S3 read/write permissions.
   ![Worker IAM Role](/img/Tao_Worker_IAM_Role.jpg)
