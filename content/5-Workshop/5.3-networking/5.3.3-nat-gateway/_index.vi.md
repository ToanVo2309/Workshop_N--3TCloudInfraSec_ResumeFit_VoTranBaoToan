---
title: "Thiết lập NAT Gateway cho Private Subnets"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3.3 </b> "
---
### 5.3.3 Thiết lập NAT Gateway cho Private Subnets

Giúp các instance ở Private Subnet kết nối ra internet một chiều (để tải package, cập nhật phần mềm) nhưng từ chối các kết nối khởi tạo từ internet đi vào.

#### Các bước thực hiện:

1. Khởi tạo hai **Elastic IP** tĩnh là `ResumeMatching-EIP` và `ResumeMatching-EIP-B`.
   ![Elastic IP A](/img/Tao_Elastic_IP.jpg)
   ![Elastic IP B](/img/Tao_Elastic_IP_B%20%28ph%C3%ADa%20sau%20b%C6%B0%E1%BB%9Bc%20t%E1%BA%A1o%20Elastic%20IP%29.jpg)
2. Tạo **NAT Gateway** tên `ResumeMatching-NAT` đặt tại `Public-Subnet-A` và gắn Elastic IP thứ nhất.
   ![NAT Gateway A](/img/Tao_NAT.jpg)
3. Tạo thêm **NAT Gateway** tên `ResumeMatching-NAT-B` đặt tại `Public-Subnet-B` và gắn Elastic IP thứ hai nhằm đảm bảo tính sẵn sàng cao (High Availability).
   ![NAT Gateway B](/img/Tao_NAT_B%20%28b%C6%B0%E1%BB%9Bc%20n%C3%A0y%20ph%C3%ADa%20sau%20b%C6%B0%E1%BB%9Bc%20t%E1%BA%A1o%20NAT%29.jpg)
4. Mở cấu hình của các Route Table Private App, thêm route `0.0.0.0/0` và trỏ `Target` về các NAT Gateway tương ứng vừa khởi tạo.
