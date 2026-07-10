---
title: "Auto Scaling Group (ASG) Provisioning"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.8.2 </b> "
---
### 5.8.2 Auto Scaling Group (ASG) Provisioning

#### Implementation Steps:

1. Create an Auto Scaling Group `ResumeMatching-ASG` and link it with the Launch Template `ResumeMatching-LT`.
2. Configure the ASG to deploy instances across private subnets: `Private-App-A` and `Private-App-B`.
3. Set the Desired capacity to `2` (Min: `2`, Max: `4`). ASG will automatically launch new EC2 instances in an initializing state for high availability and load distribution.
   ![Create ASG](/img/Tao_ASG.jpg)
