---
title: "Cấu hình Subnet và Route Table"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.3.2 </b> "
---
### 5.3.2 Cấu hình Subnet và Route Table

Chia nhỏ dải mạng VPC thành các mạng con để phân tách các tầng ứng dụng (Public cho Load Balancer, Private App cho EC2, Private DB cho RDS).

#### Các bước thực hiện:

1. Truy cập mục **Subnets** và tạo lần lượt các subnet với các dải CIDR phù hợp:
   * Public Subnets: `Public-Subnet-A` (`10.0.1.0/24`), `Public-Subnet-B` (`10.0.2.0/24`).
   * Private App Subnets: `Private-App-A` (`10.0.11.0/24`), `Private-App-B` (`10.0.12.0/24`).
   * Private DB Subnets: `Private-DB-A` (`10.0.21.0/24`), `Private-DB-B` (`10.0.22.0/24`).
   ![Subnets List](/img/Tao_cac_Public_va_Private_subnet.jpg)

2. Tạo một Route Table công khai với tên `Public-RT` và gán vào VPC.
   ![Public Route Table](/img/Tao_Public_Route_Table.jpg)
3. Trong phần **Edit routes** của `Public-RT`, thêm route có `Destination` là `0.0.0.0/0` và trỏ `Target` đến Internet Gateway (`igw-...`).
   ![Add Route](/img/Add_Routes.jpg)
4. Gán (Associate) `Public-RT` vào 2 subnets: `Public-Subnet-A` và `Public-Subnet-B`.
   ![Associate Public RT](/img/Gan_Public_Route_Table.jpg)

5. Tạo thêm các Route Table riêng tư:
   * `Private-App-RT`: Gán cho `Private-App-A` và Private-App-B.
     ![Private App RT A](/img/Tao_va_gan_Private_App_Route_Table.jpg)
     ![Associate App A](/img/Add_Route_Tables_cho_Private-App-RT.jpg)
   * `ResumeMatching-Private-App-RT-B`: Gán cho `Private-App-B`.
     ![Private App RT B](/img/Tao_Route_Table_B.jpg)
   * `Private-DB-RT`: Gán cho cả 2 DB Subnet `Private-DB-A` và `Private-DB-B`.
     ![Private DB RT](/img/Tao_va_gan_Database_Route_Table.jpg)
