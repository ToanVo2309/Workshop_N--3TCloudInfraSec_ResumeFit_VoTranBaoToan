---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:
* Tìm hiểu ảo hóa cơ sở dữ liệu quan hệ với dịch vụ Amazon RDS.
* Bảo mật cơ sở dữ liệu bên trong Private Subnet và cấu hình phân quyền truy xuất.
* Cấu hình chính sách sao lưu tự động, tạo Snapshot thủ công và thực hành khôi phục dữ liệu.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | ------------ | --------------- | -------------- |
| Thứ 2 | Tìm hiểu các Database Engine trên RDS (MySQL/PostgreSQL), các loại Storage và DB Subnet Group. | 25/05/2026 | 25/05/2026 | [Video](https://www.youtube.com/watch?v=hZ-kH52vdfg) <br> [Tài liệu cơ sở dữ liệu RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html) |
| Thứ 3 | Nghiên cứu cơ chế dự phòng Multi-AZ (High Availability) và nhân bản đọc Read Replica. | 26/05/2026 | 26/05/2026 | [Cơ chế dự phòng Multi-AZ](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html) |
| Thứ 4 | Thực hành tạo RDS MySQL Instance nằm hoàn toàn trong Private Subnet sử dụng Subnet Group. | 27/05/2026 | 27/05/2026 | [Triển khai RDS trong VPC](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html) |
| Thứ 5 | Cấu hình Security Group của RDS chỉ cho phép duy nhất các máy chủ Web EC2 kết nối vào cổng database. | 28/05/2026 | 28/05/2026 | [Kết nối EC2 tới cơ sở dữ liệu RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.Scenarios.html) |
| Thứ 6 | Thiết lập backup tự động, tạo thử một bản DB Snapshot thủ công và thực hành khôi phục cơ sở dữ liệu. | 29/05/2026 | 29/05/2026 | [Sao lưu và Khôi phục RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithAutomatedBackups.html) |

### Kết quả đạt được tuần 6:
* Khởi tạo thành công hệ thống cơ sở dữ liệu quan hệ được bảo vệ đa lớp theo tiêu chuẩn bảo mật.
* Cô lập hoàn toàn truy cập từ bên ngoài Internet vào DB, chỉ cho phép kết nối nội bộ từ ứng dụng web.
* Nắm vững nguyên lý hoạt động của cấu hình Multi-AZ tự động đồng bộ dữ liệu dự phòng.
* Thực hiện thành công việc sao lưu và khôi phục dữ liệu từ Snapshot để sẵn sàng ứng phó sự cố.
