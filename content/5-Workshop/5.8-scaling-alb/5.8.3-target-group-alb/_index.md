---
title: "Target Group and Load Balancer Setup"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.8.3 </b> "
---
### 5.8.3 Target Group and Load Balancer Setup

#### Implementation Steps:

1. Create a **Target Group** named `ResumeMatching-TG` of type `Instance` for HTTP traffic on port `8080`.
   ![Create Target Group](/img/Tao_target_group.jpg)
2. Provision an **Application Load Balancer (ALB)** named `ResumeMatching-ALB`. Set its scheme to `Internet-facing` to handle public user traffic, associate it with `Public-Subnet-A` and `Public-Subnet-B`, and forward traffic to the Target Group.
   ![Create ALB](/img/Tao_ALB.jpg)
