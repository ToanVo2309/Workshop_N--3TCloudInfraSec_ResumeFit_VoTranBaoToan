---
title: "Dọn dẹp tài nguyên"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---
### 5.11. Dọn dẹp tài nguyên

Sau khi hoàn tất quá trình thực hiện bài lab và kiểm thử, để tránh phát sinh thêm chi phí duy trì hạ tầng không cần thiết trên AWS, hãy thực hiện dọn dẹp các tài nguyên theo thứ tự dưới đây:

1. **Auto Scaling Group**: Xóa Auto Scaling Group trước để ngăn chặn nó tự động khởi tạo lại máy chủ mới. Tiến hành Terminate các instance thủ công còn lại.
2. **Cân bằng tải (ALB)**: Xóa Application Load Balancer và Target Group liên quan.
3. **Cơ sở dữ liệu (RDS)**: Xóa PostgreSQL DB Instance. Bỏ chọn tùy chọn tạo final snapshot nếu bạn không muốn lưu giữ dữ liệu. Sau khi database bị xóa, tiến hành xóa DB Subnet Group.
4. **NAT Gateway**: Xóa các NAT Gateways đã tạo. Đợi trạng thái NAT Gateway chuyển hẳn sang `Deleted`, sau đó tiến hành Release các Elastic IP tĩnh.
5. **Hạ tầng Mạng (VPC)**: Giải phóng VPC Endpoints, Route Tables, Internet Gateway, Subnets và cuối cùng là xóa VPC `ResumeMatching-VPC`.
6. **Lưu trữ S3**: Truy cập S3, xóa rỗng (Empty) toàn bộ đối tượng trong bucket `resume-matching-storage-...` và sau đó xóa bucket.
7. **Secrets & IAM**: Xóa các Secrets đã lưu trữ trên Secrets Manager và các IAM Roles/Policies liên quan nếu không có nhu cầu sử dụng tiếp.
