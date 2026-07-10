---
title: "Create VPC and Internet Gateway"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.3.1 </b> "
---
### 5.3.1 Create VPC and Internet Gateway

An isolated Virtual Private Cloud (VPC) provides a secure foundation for the entire application, controlling all network traffic.

#### Implementation Steps:

1. Access the VPC Console, click **Create VPC**.
2. Initialize a VPC named `ResumeMatching-VPC` with IPv4 CIDR block `10.0.0.0/16`.
   ![VPC Creation](/img/tao_VPC.jpg)
3. Create an Internet Gateway named `ResumeMatching-IGW` to provide internet connectivity for public resources.
   ![Internet Gateway](/img/Tao_Internet_Gateway.jpg)
4. Attach the created Internet Gateway to `ResumeMatching-VPC`.
   ![Attach IGW](/img/Attach_vao_VPC.jpg)
5. Under your VPC settings, enable **Enable DNS hostnames** to support local hostname resolutions.
   ![Enable DNS Hostnames](/img/Enable_DNS_Hostnames.jpg)
