---
title: "Kiểm tra hoạt động của Auto Scaling Group"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.9.1 </b> "
---
### 5.9.1 Kiểm tra hoạt động của Auto Scaling Group

#### Các bước thực hiện:

1. Truy cập dịch vụ **EC2**, điều hướng đến menu **Instances**.
2. Quan sát hệ thống tự động khởi tạo các EC2 mới có tiền tố `ResumeMatching-ASG-Instance` phân bổ đều ở các Availability Zone khác nhau.
   ![ASG Spawning EC2](/img/ASG_tao_them_EC2.jpg)
3. Một số máy chủ cũ có thể hiển thị trạng thái `Terminated`. Đây là minh chứng ASG đang hoạt động chính xác: tự động thu hồi máy chủ cũ và khởi chạy máy chủ mới khi có sự thay đổi cấu hình hoặc lỗi hệ thống.
   ![ASG New EC2](/img/ASG_tao_EC2_moi_sau%20khi_cap_nhat_AMI.jpg)
