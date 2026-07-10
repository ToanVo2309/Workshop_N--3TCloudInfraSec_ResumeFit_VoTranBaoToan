---
title: "Launch EC2 Backend Instance"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.7.1 </b> "
---
### 5.7.1 Launch EC2 Backend Instance

#### Implementation Steps:

1. Create a **Key Pair** (`ResumeMatching-Key`) of type RSA for SSH access.
   ![Create Key Pair](/img/Tao_Key_Pair.jpg)
2. In the EC2 Dashboard, launch an instance named `ResumeMatching-Backend` using `t3.micro` instance type. Deploy it in the VPC's `Private-App-A` subnet, and associate `ResumeMatching-Backend-Role` and `ResumeMatching-Backend-SG`.
   ![Launch EC2](/img/Tao_EC2_Backend.jpg)
3. Wait until the Instance State is `Running` and Status Check shows `2/2 checks passed`.
