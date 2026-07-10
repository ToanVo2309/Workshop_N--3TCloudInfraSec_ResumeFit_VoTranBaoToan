---
title: "Giám sát hiệu suất qua CloudWatch"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.9.3 </b> "
---
### 5.9.3 Giám sát hiệu suất qua CloudWatch

#### Các bước thực hiện:

1. Truy cập **CloudWatch**, chọn menu **Metrics** để giám sát sâu các thông số.
2. **Đối với EC2**: Lọc Namespace EC2, chọn `CPUUtilization`. Quan sát biểu đồ để thấy các đỉnh xử lý (ví dụ `81.9%`) khi AI chạy tác vụ nặng, từ đó thiết lập Threshold mở rộng tự động cho ASG.
   ![CloudWatch EC2](/img/CloudWatch_dang_monitor_EC2.jpg)
   ![EC2 CPU Metrics](/img/EC2_Metrics.jpg)
3. **Đối với ALB**: Lọc metric `RequestCount` và `TargetResponseTime`. Sự tương quan giữa việc tăng vọt lượng Request và sự thay đổi của thời gian phản hồi (ví dụ `660.4 ms`) giúp đánh giá tính trơn tru của trải nghiệm người dùng.
   ![CloudWatch ALB](/img/CloudWatch_monitor_Load_Balancer.jpg)
   ![ALB Metrics](/img/ALB_Metrics.jpg)
