---
title: "Khởi tạo EC2 Backend Instance"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.7.1 </b> "
---
### 5.7.1 Khởi tạo EC2 Backend Instance

#### Các bước thực hiện:

1. Tạo một khóa **Key Pair** (`ResumeMatching-Key`) kiểu RSA để kết nối SSH.
   ![Create Key Pair](/img/Tao_Key_Pair.jpg)
2. Tại EC2 Dashboard, khởi chạy một Instance có tên `ResumeMatching-Backend` với Instance type là `t3.micro` đặt trong VPC ứng dụng (`Private-App-A`), gán IAM Role `ResumeMatching-Backend-Role` và Security Group `ResumeMatching-Backend-SG`.
   ![Launch EC2](/img/Tao_EC2_Backend.jpg)
3. Đợi trạng thái Instance chuyển sang `Running` và Status check hiển thị `2/2 checks passed`.
