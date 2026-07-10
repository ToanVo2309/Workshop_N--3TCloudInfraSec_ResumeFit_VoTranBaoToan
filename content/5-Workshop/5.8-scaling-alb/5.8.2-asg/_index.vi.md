---
title: "Auto Scaling Group (ASG)"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.8.2 </b> "
---
### 5.8.2 Auto Scaling Group (ASG)

#### Các bước thực hiện:

1. Tạo Auto Scaling Group `ResumeMatching-ASG` và liên kết với Launch template `ResumeMatching-LT`.
2. Gán ASG chạy trong 2 subnet private: `Private-App-A` và `Private-App-B` để đảm bảo dự phòng.
3. Chỉnh sửa Desired capacity lên thành `2` (Min: `2`, Max: `4`). ASG sẽ tự động khởi chạy các EC2 instances mới ở trạng thái Initializing nhằm phục vụ mở rộng tải khi cần thiết.
   ![Create ASG](/img/Tao_ASG.jpg)
