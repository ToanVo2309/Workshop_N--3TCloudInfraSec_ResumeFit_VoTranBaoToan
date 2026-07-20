---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---
# Triển khai AI Resume Matching & Interview Preparation Platform trên AWS

#### Tổng quan

Bài lab này hướng dẫn chi tiết cách triển khai toàn diện hệ thống **Resume Fit** trên nền tảng đám mây AWS. Resume Fit là một ứng dụng AI giúp đánh giá độ phù hợp giữa Hồ sơ ứng viên (CV) và Yêu cầu công việc (JD) một cách nhanh chóng, minh bạch nhằm hỗ trợ ra quyết định tuyển dụng.

Hệ thống được thiết kế theo kiến trúc chuẩn trên AWS, đảm bảo tính mở rộng và sẵn sàng cao.

#### 1. Source code và Demo
- **1.1 Link demo Resume Fit:** [http://resumematching-alb-1223673352.us-east-1.elb.amazonaws.com](http://resumematching-alb-1223673352.us-east-1.elb.amazonaws.com)
- **1.2 Link source code Resume Fit:** [https://github.com/thuanthien-tran/resume-fit](https://github.com/thuanthien-tran/resume-fit)

#### 2. Các dịch vụ AWS sử dụng trong dự án
Hệ thống tận dụng các dịch vụ đám mây cốt lõi của AWS để đảm bảo khả năng sẵn sàng cao và bảo mật:
- **Mạng cô lập (VPC & Security)**: [5.3. Xây dựng mạng ảo VPC](5.3-networking/) & [5.4. Cấu hình Bảo mật và IAM Policies](5.4-security/)
- **Lưu trữ & Hàng đợi bất đồng bộ**: [5.5. Thiết lập Lưu trữ S3 và Hàng đợi SQS](5.5-storage-queue/)
- **Cơ sở dữ liệu quan hệ (PostgreSQL)**: [5.6. Cấu hình RDS PostgreSQL](5.6-database/)
- **Máy chủ tính toán & Co giãn tự động**: [5.7. Triển khai các Instance EC2](5.7-compute/) & [5.8. Tự động mở rộng và Cân bằng tải](5.8-scaling-alb/)
- **Giám sát & Quản lý Secret**: [5.9. Giám sát Hệ thống (Observability)](5.9-monitoring/)

#### 3. Phát triển và Triển khai (Development and Deployment)
- Quản lý mã nguồn trên GitHub và thực hiện quy trình triển khai ứng dụng dạng Docker container trên nền máy chủ Amazon EC2:
  - Chi tiết khởi tạo cụm máy chủ Backend & Worker: [5.7. Triển khai các Instance EC2](5.7-compute/)
  - Cấu hình Launch Template, Target Group và Application Load Balancer (ALB): [5.8. Tự động mở rộng và Cân bằng tải](5.8-scaling-alb/)
  - Kiểm thử và xác minh tính sẵn sàng của toàn bộ ứng dụng: [5.10. Kiểm thử Ứng dụng](5.10-testing/)

#### 4. Chi phí và Dọn dẹp tài nguyên (Cost and Resource Cleanup)
- Báo cáo ước tính chi phí triển khai hệ thống (AWS Pricing Calculator) và các bước giải phóng tài nguyên tránh phát sinh chi phí:
  - Tham khảo chi tiết tại: [5.11. Dọn dẹp tài nguyên và Phân tích chi phí](5.11-cleanup/)

---

#### Nội dung bài lab

1. [5.1. Giới thiệu](5.1-intro/)
2. [5.2. Các bước chuẩn bị](5.2-prerequisites/)
3. [5.3. Xây dựng mạng ảo VPC](5.3-networking/)
4. [5.4. Cấu hình Bảo mật và IAM Policies](5.4-security/)
5. [5.5. Thiết lập Lưu trữ S3 và Hàng đợi SQS](5.5-storage-queue/)
6. [5.6. Cấu hình RDS PostgreSQL](5.6-database/)
7. [5.7. Triển khai các Instance EC2](5.7-compute/)
8. [5.8. Tự động mở rộng và Cân bằng tải](5.8-scaling-alb/)
9. [5.9. Giám sát Hệ thống (Observability)](5.9-monitoring/)
10. [5.10. Kiểm thử Ứng dụng](5.10-testing/)
11. [5.11. Dọn dẹp tài nguyên và Phân tích chi phí](5.11-cleanup/)
