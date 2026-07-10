---
title: "Cấu hình AMI và Launch Template"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.8.1 </b> "
---
### 5.8.1 Cấu hình AMI và Launch Template

#### Các bước thực hiện:

1. Chuẩn hóa môi trường EC2 vừa cài đặt bằng cách tạo ra một Amazon Machine Image (AMI) mang tên `ResumeMatching-Backend-AMI`.
   ![Create AMI](/img/Tao_AMIs.jpg)
2. Từ AMI này, tạo một **Launch Template** mang tên `ResumeMatching-LT` chứa các cấu hình phần cứng, subnet, IAM role và bảo mật chuẩn.
   ![Create Launch Template](/img/Tao_launch_template.jpg)
