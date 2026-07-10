---
title: "Provision NAT Gateways for Private Subnets"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3.3 </b> "
---
### 5.3.3 Provision NAT Gateways for Private Subnets

Allows private subnet instances to connect one-way to the internet (to download packages, run updates) while blocking incoming connection requests from the internet.

#### Implementation Steps:

1. Allocate two static **Elastic IP** addresses: `ResumeMatching-EIP` and `ResumeMatching-EIP-B`.
   ![Elastic IP A](/img/Tao_Elastic_IP.jpg)
   ![Elastic IP B](/img/Tao_Elastic_IP_B%20%28ph%C3%ADa%20sau%20b%C6%B0%E1%BB%9Bc%20t%E1%BA%A1o%20Elastic%20IP%29.jpg)
2. Create a **NAT Gateway** named `ResumeMatching-NAT` placed in `Public-Subnet-A` and bind it to the first Elastic IP.
   ![NAT Gateway A](/img/Tao_NAT.jpg)
3. Create an additional **NAT Gateway** named `ResumeMatching-NAT-B` placed in `Public-Subnet-B` and bind it to the second Elastic IP to ensure High Availability.
   ![NAT Gateway B](/img/Tao_NAT_B%20%28b%C6%B0%E1%BB%9Bc%20n%C3%A0y%20ph%C3%ADa%20sau%20b%C6%B0%E1%BB%9Bc%20t%E1%BA%A1o%20NAT%29.jpg)
4. Open your Private App Route Tables, add a route for `0.0.0.0/0` pointing to the respective NAT Gateways.
