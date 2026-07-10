---
title: "Kiểm tra Health Check của Target Group"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.9.2 </b> "
---
### 5.9.2 Kiểm tra Health Check của Target Group

#### Các bước thực hiện:

1. Tại mục **Load Balancing**, chọn **Target Groups**, nhấn chọn vào Target Group của hệ thống.
2. Chuyển sang tab **Targets** và quan sát bảng **Registered targets**.
3. Xác nhận cột `Health status` của các instance hiển thị trạng thái màu xanh `Healthy`, chứng minh máy chủ web đã khởi động và sẵn sàng nhận request từ Load Balancer.
   ![Target Group Healthy](/img/Target_group_healthy_check.jpg)
