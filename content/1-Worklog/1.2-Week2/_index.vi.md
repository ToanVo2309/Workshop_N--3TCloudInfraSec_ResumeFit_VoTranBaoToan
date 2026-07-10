---
title: "Worklog Tuần 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:
* Tìm hiểu dịch vụ tính toán cốt lõi Amazon EC2, lưu trữ đối tượng Amazon S3 và quản trị truy cập IAM.
* Hiểu phương thức kết nối SSH key pair và cấu hình tường lửa Security Group cơ bản.
* Áp dụng IAM Policy để phân quyền chi tiết cho người dùng và tài nguyên hệ thống.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | ------------ | --------------- | -------------- |
| Thứ 2 | Nghiên cứu các thành phần IAM: User, Group, Role, Policy và nguyên lý đặc quyền tối thiểu. | 27/04/2026 | 27/04/2026 | [Video](https://www.youtube.com/watch?v=7X16cZlWfO8) <br> [Tổng quan về AWS IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) |
| Thứ 3 | Tìm hiểu lý thuyết EC2: các loại Instance, AMI, EBS Volume, Key Pair và Security Group. | 28/04/2026 | 28/04/2026 | [Khái niệm cơ bản về EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html) |
| Thứ 4 | Thực hành tạo EC2 Linux Instance, cấu hình Security Group và kết nối SSH từ máy cá nhân. | 29/04/2026 | 29/04/2026 | [Kết nối SSH vào EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstances.html) |
| Thứ 5 | Nghiên cứu lý thuyết Amazon S3: Bucket, Object, các lớp lưu trữ, Versioning và Bucket Policy. | 30/04/2026 | 30/04/2026 | [Quản lý Amazon S3 Bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingBucket.html) |
| Thứ 6 | Thực hành tạo S3 Bucket, upload tài liệu và cấu hình phân quyền truy cập thông qua IAM Role. | 01/05/2026 | 01/05/2026 | [Cấp quyền IAM Role cho EC2](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2.html) |

### Kết quả đạt được tuần 2:
* Nắm vững cơ chế bảo mật phân quyền AWS sử dụng IAM User và các IAM Policy tự định nghĩa.
* Tạo lập và kết nối từ xa thành công vào máy chủ ảo EC2 bằng SSH key an toàn.
* Triển khai lưu trữ trên Amazon S3 với cơ chế bảo mật phân quyền đọc ghi chặt chẽ.
* Liên kết phân quyền an toàn giữa máy chủ EC2 và bộ lưu trữ S3 thông qua việc gán IAM Role.
