---
title: "Worklog Tuần 5"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:
* Triển khai kiến trúc có tính sẵn sàng cao thông qua bộ cân bằng tải Application Load Balancer (ALB).
* Cấu hình Auto Scaling Group (ASG) tự động co giãn số lượng máy chủ theo tải thực tế.
* Tích hợp AWS WAF phía trước bộ cân bằng tải để lọc và chặn các truy cập độc hại.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | ------------ | --------------- | -------------- |
| Thứ 2 | Nghiên cứu nguyên lý hoạt động của Application Load Balancer, Target Group và cơ chế Health Check. | 18/05/2026 | 18/05/2026 | [Video](https://www.youtube.com/watch?v=Vl03U1jF4gI) <br> [Giới thiệu Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html) |
| Thứ 3 | Tìm hiểu thành phần Auto Scaling Group: Launch Template, Scaling Policy và thời gian chờ Cooldown. | 19/05/2026 | 19/05/2026 | [Khái niệm Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html) |
| Thứ 4 | Thực hành tạo ALB và cấu hình phân phối tải đều sang các máy chủ web EC2 ở các AZ khác nhau. | 20/05/2026 | 20/05/2026 | [Hướng dẫn cấu hình ALB](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/application-load-balancer-getting-started.html) |
| Thứ 5 | Tạo ASG thiết lập ngưỡng tự động tăng giảm số lượng máy chủ dựa trên chỉ số CPU tiêu thụ. | 21/05/2026 | 21/05/2026 | [Chính sách co giãn Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-scaling-target-tracking.html) |
| Thứ 6 | Gắn AWS WAF chặn các truy cập IP xấu vào ALB và chạy script giả lập tải để kiểm tra tính co giãn. | 22/05/2026 | 22/05/2026 | [Tài liệu lập trình AWS WAF](https://docs.aws.amazon.com/waf/latest/developerguide/waf-chapter.html) |

### Kết quả đạt được tuần 5:
* Xây dựng thành công hệ thống Web có khả năng chịu lỗi trên nhiều vùng sẵn sàng (Multi-AZ).
* Cấu hình cơ chế tự sửa lỗi (Self-healing) tự động thay thế máy chủ bị hỏng thông qua Health Check.
* Thiết lập thành công chính sách co giãn tự động linh hoạt giúp tối ưu chi phí hạ tầng.
* Bảo vệ thành công cổng truy cập chính ALB khỏi các cuộc tấn công SQL Injection và DDoS cơ bản.
