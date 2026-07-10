---
title: "Target Group và Application Load Balancer"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.8.3 </b> "
---
### 5.8.3 Target Group và Application Load Balancer

#### Các bước thực hiện:

1. Tạo một **Target Group** tên `ResumeMatching-TG`, dạng `Instance` chạy giao thức HTTP trên cổng `8080`.
   ![Create Target Group](/img/Tao_target_group.jpg)
2. Khởi tạo **Application Load Balancer (ALB)** tên `ResumeMatching-ALB`. Lựa chọn Scheme là `Internet-facing` để nhận traffic từ ngoài internet, gán các subnet công khai `Public-Subnet-A`, `Public-Subnet-B` và định tuyến giao thông vào Target Group.
   ![Create ALB](/img/Tao_ALB.jpg)
