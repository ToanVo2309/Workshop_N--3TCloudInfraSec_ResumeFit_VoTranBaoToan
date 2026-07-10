---
title: "Khởi tạo Security Groups"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.4.1 </b> "
---
### 5.4.1 Khởi tạo Security Groups

Thiết lập tường lửa ảo kiểm soát luồng giao thông mạng giữa các tài nguyên ở mức độ giao thức và cổng kết nối.

#### Các bước thực hiện:

1. **ALB Security Group** (`ResumeMatching-ALB-SG`): Mở port HTTP (`80`) và HTTPS (`443`) (TCP) với Source là `0.0.0.0/0` để cho phép người dùng truy cập ứng dụng từ internet.
   ![ALB Security Group](/img/Tao_ALB_Security_Group.jpg)
2. **Backend Security Group** (`ResumeMatching-Backend-SG`): Cấu hình Inbound rule cho phép giao thức HTTP trên cổng `8080`. Source được giới hạn chỉ nhận luồng từ `ResumeMatching-ALB-SG`.
   ![Backend Security Group](/img/Tao_Backend_Security_Group.jpg)
3. **Worker Security Group** (`ResumeMatching-Worker-SG`): Tường lửa bảo vệ Worker Server xử lý tác vụ nền.
   ![Worker Security Group](/img/T%E1%BA%A1o_Worker_Security_Group.jpg)
4. **Database Security Group** (`ResumeMatching-RDS-SG`): Mở port `5432` (PostgreSQL). Source chỉ cho phép nhận kết nối nội bộ từ Backend và Worker Security Group.
   ![Database Security Group](/img/Tao_Database_Security_Group.jpg)
