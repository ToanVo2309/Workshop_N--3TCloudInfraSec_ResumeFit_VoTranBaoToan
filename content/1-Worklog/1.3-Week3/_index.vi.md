---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:
* Hiểu cấu trúc mạng ảo riêng biệt trên AWS với dịch vụ Virtual Private Cloud (VPC).
* Cấu hình phân chia Public và Private Subnet, Route Table và cổng Internet Gateway.
* Thiết lập bảo mật hai lớp cho hệ thống mạng sử dụng Security Group và Network ACL.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | ------------ | --------------- | -------------- |
| Thứ 2 | Tìm hiểu lý thuyết VPC: dải địa chỉ CIDR, Subnet, cổng Internet Gateway (IGW) và Route Table. | 04/05/2026 | 04/05/2026 | [Video](https://www.youtube.com/watch?v=jZNv98SyP_c) <br> [Giới thiệu Amazon VPC](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html) |
| Thứ 3 | Nghiên cứu vai trò của NAT Gateway để hỗ trợ Private Subnet đi Internet một chiều. | 05/05/2026 | 05/05/2026 | [Cấu hình NAT Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) |
| Thứ 4 | Thực hành tự thiết kế VPC cá nhân, tạo các Public và Private Subnet cùng bảng định tuyến tương ứng. | 06/05/2026 | 06/05/2026 | [Khởi tạo VPC tùy chỉnh](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-vpcs.html) |
| Thứ 5 | Phân tích sự khác biệt hoạt động giữa Security Group (Stateful) và Network ACL (Stateless). | 07/05/2026 | 07/05/2026 | [Bảo mật Security Group và NACL](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Security.html) |
| Thứ 6 | Khởi chạy EC2 trong cả hai Subnet và kiểm tra kết nối định tuyến đi Internet thực tế. | 08/05/2026 | 08/05/2026 | [Khắc phục lỗi kết nối EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/TroubleshootingInstancesConnecting.html) |

### Kết quả đạt được tuần 3:
* Tự thiết kế và thiết lập thành công hệ thống mạng VPC tùy chỉnh từ con số không.
* Nắm vững kiến thức phân vùng mạng để tách biệt tầng Web công cộng và tầng Cơ sở dữ liệu nội bộ.
* Cấu hình thành công NAT Gateway cho phép máy chủ trong Private Subnet kết nối ra Internet để cập nhật phần mềm.
* Áp dụng hiệu quả bộ quy tắc lọc gói tin tại tầng máy chủ (Security Group) và tầng mạng (NACL).
