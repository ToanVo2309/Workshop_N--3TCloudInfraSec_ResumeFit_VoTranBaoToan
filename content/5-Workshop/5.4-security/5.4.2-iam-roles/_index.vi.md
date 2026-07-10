---
title: "Cấu hình IAM Roles"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.4.2 </b> "
---
### 5.4.2 Cấu hình IAM Roles

Cấp quyền ủy quyền an toàn cho các máy chủ EC2 giao tiếp với các dịch vụ AWS khác mà không cần lưu trữ Hard-code Access Key.

#### Các bước thực hiện:

1. Truy cập dịch vụ **IAM**, tạo role `ResumeMatching-Backend-Role` để cấp cho máy chủ backend chạy trên EC2, cho phép đọc cấu hình và dữ liệu an toàn.
   ![Backend IAM Role](/img/Tao_Backend_IAM_Role.jpg)
2. Tạo role thứ hai mang tên `ResumeMatching-Worker-Role` dành riêng cho Worker server. Đính kèm các policy AWS Managed như `AmazonSQSFullAccess` và quyền thao tác với S3.
   ![Worker IAM Role](/img/Tao_Worker_IAM_Role.jpg)
