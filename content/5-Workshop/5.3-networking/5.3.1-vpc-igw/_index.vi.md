---
title: "Tạo VPC và Internet Gateway"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.3.1 </b> "
---
### 5.3.1 Tạo VPC và Internet Gateway

Hạ tầng mạng cô lập (VPC) là nền tảng bảo mật vững chắc cho toàn bộ ứng dụng, giúp kiểm soát hoàn toàn luồng giao thông mạng.

#### Các bước thực hiện:

1. Truy cập vào giao diện VPC Console, chọn **Create VPC**.
2. Khởi tạo một VPC với tên `ResumeMatching-VPC` và thiết lập dải IP `IPv4 CIDR` là `10.0.0.0/16`.
   ![VPC Creation](/img/tao_VPC.jpg)
3. Tạo một Internet Gateway có tên `ResumeMatching-IGW` để cung cấp đường truyền kết nối ra internet cho các tài nguyên công khai.
   ![Internet Gateway](/img/Tao_Internet_Gateway.jpg)
4. Thực hiện Attach Internet Gateway vừa tạo vào `ResumeMatching-VPC`.
   ![Attach IGW](/img/Attach_vao_VPC.jpg)
5. Mở VPC vừa tạo, chỉnh sửa DNS Settings và bật **Enable DNS hostnames** để hỗ trợ phân giải tên miền nội bộ.
   ![Enable DNS Hostnames](/img/Enable_DNS_Hostnames.jpg)
