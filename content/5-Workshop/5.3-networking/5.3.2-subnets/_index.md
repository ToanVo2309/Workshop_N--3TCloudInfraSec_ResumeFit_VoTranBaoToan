---
title: "Subnet and Route Table Configurations"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.3.2 </b> "
---
### 5.3.2 Subnet and Route Table Configurations

Divide the VPC network block into subnets to segregate application layers (Public for Load Balancers, Private App for EC2s, Private DB for RDS PostgreSQL).

#### Implementation Steps:

1. Go to **Subnets** and create subnets with appropriate CIDR blocks:
   * Public Subnets: `Public-Subnet-A` (`10.0.1.0/24`), `Public-Subnet-B` (`10.0.2.0/24`).
   * Private App Subnets: `Private-App-A` (`10.0.11.0/24`), `Private-App-B` (`10.0.12.0/24`).
   * Private DB Subnets: `Private-DB-A` (`10.0.21.0/24`), `Private-DB-B` (`10.0.22.0/24`).
   ![Subnets List](/img/Tao_cac_Public_va_Private_subnet.jpg)

2. Create a public Route Table named `Public-RT` and associate it with the VPC.
   ![Public Route Table](/img/Tao_Public_Route_Table.jpg)
3. In the **Edit routes** section of `Public-RT`, add a route with Destination `0.0.0.0/0` targeting the Internet Gateway (`igw-...`).
   ![Add Route](/img/Add_Routes.jpg)
4. Associate `Public-RT` with `Public-Subnet-A` and `Public-Subnet-B`.
   ![Associate Public RT](/img/Gan_Public_Route_Table.jpg)

5. Create private Route Tables:
   * `Private-App-RT`: Associate with `Private-App-A` and Private-App-B.
     ![Private App RT A](/img/Tao_va_gan_Private_App_Route_Table.jpg)
     ![Associate App A](/img/Add_Route_Tables_cho_Private-App-RT.jpg)
   * `ResumeMatching-Private-App-RT-B`: Associate with `Private-App-B`.
     ![Private App RT B](/img/Tao_Route_Table_B.jpg)
   * `Private-DB-RT`: Associate with DB subnets `Private-DB-A` and `Private-DB-B`.
     ![Private DB RT](/img/Tao_va_gan_Database_Route_Table.jpg)
