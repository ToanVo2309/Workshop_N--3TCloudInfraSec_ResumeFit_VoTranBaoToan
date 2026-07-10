---
title: "AMI Creation and Launch Template Setup"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.8.1 </b> "
---
### 5.8.1 AMI Creation and Launch Template Setup

#### Implementation Steps:

1. Standarize the EC2 environment by creating an Amazon Machine Image (AMI) named `ResumeMatching-Backend-AMI`.
   ![Create AMI](/img/Tao_AMIs.jpg)
2. From this AMI, create a **Launch Template** named `ResumeMatching-LT` defining hardware configurations, private subnets, security group, and backend IAM role.
   ![Create Launch Template](/img/Tao_launch_template.jpg)
