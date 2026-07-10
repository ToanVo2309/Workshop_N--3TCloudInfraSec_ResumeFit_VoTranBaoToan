---
title: "Worklog Tuần 4"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:
* Triển khai giám sát hạ tầng bằng CloudWatch và ghi nhật ký hoạt động hệ thống bằng CloudTrail.
* Bảo vệ ứng dụng web trước các đợt tấn công bằng AWS WAF và mã hóa dữ liệu nhạy cảm bằng AWS KMS.
* Đánh giá và tối ưu hóa quyền hạn truy cập tài nguyên thông qua IAM Access Analyzer.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | ------------ | --------------- | -------------- |
| Thứ 2 | Tìm hiểu hệ thống CloudWatch (Metric, Dashboard, Alarm, Logs) và hệ thống kiểm toán API CloudTrail. | 11/05/2026 | 11/05/2026 | [Video](https://www.youtube.com/watch?v=aG3_5CevQ1E) <br> [Giới thiệu Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html) |
| Thứ 3 | Nghiên cứu nguyên lý hoạt động của AWS WAF (Web ACLs) và dịch vụ quản lý khóa mã hóa AWS KMS. | 12/05/2026 | 12/05/2026 | [Hướng dẫn AWS CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html) |
| Thứ 4 | Thực hành tạo CloudWatch Alarm giám sát chỉ số CPU của EC2 và gửi cảnh báo qua email (SNS). | 13/05/2026 | 13/05/2026 | [Thiết lập CloudWatch Alarm](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/ConsoleAlarms.html) |
| Thứ 5 | Tạo khóa mã hóa tùy chỉnh (CMK) bằng KMS và thực hành mã hóa tệp dữ liệu tải lên S3. | 14/05/2026 | 14/05/2026 | [Tổng quan mã hóa AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html) |
| Thứ 6 | Chạy IAM Access Analyzer để quét phát hiện các tài nguyên đang bị phân quyền mở rộng ra bên ngoài. | 15/05/2026 | 15/05/2026 | [Phân tích quyền với Access Analyzer](https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html) |

### Kết quả đạt được tuần 4:
* Xây dựng thành công cơ chế giám sát hiệu năng máy chủ và ghi nhận logs thời gian thực.
* Thiết lập kênh gửi thông báo cảnh báo tự động qua email khi máy chủ gặp sự cố quá tải.
* Mã hóa thành công dữ liệu lưu trữ tĩnh (Data-at-rest) trên Amazon S3 dùng khóa bảo mật tự quản lý.
* Phân tích và khắc phục các lỗ hổng phân quyền tài nguyên mở qua kết quả của IAM Access Analyzer.
