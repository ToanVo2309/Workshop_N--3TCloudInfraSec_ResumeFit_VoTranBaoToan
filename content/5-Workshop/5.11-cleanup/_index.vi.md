---
title: "Dọn dẹp tài nguyên"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---
### 5.11. Dọn dẹp tài nguyên và Dự tính Chi phí

#### 1. Quy trình Dọn dẹp Tài nguyên (Resource Cleanup)

Sau khi hoàn tất quá trình thực hiện bài lab và kiểm thử, để tránh phát sinh thêm chi phí duy trì hạ tầng không cần thiết trên AWS, hãy thực hiện dọn dẹp các tài nguyên theo thứ tự dưới đây:

1. **Auto Scaling Group**: Xóa Auto Scaling Group trước để ngăn chặn tự động khởi tạo máy chủ mới. Tiến hành Terminate các instance EC2 thủ công còn lại.
2. **Cân bằng tải (ALB)**: Xóa Application Load Balancer và Target Group liên quan.
3. **Cơ sở dữ liệu (RDS)**: Xóa PostgreSQL DB Instance. Bỏ chọn tùy chọn tạo final snapshot nếu không muốn lưu giữ dữ liệu. Xóa DB Subnet Group sau khi database bị xóa.
4. **NAT Gateway**: Xóa các NAT Gateways đã tạo. Đợi trạng thái NAT Gateway chuyển sang `Deleted`, sau đó tiến hành Release các Elastic IP tĩnh.
5. **Hạ tầng Mạng (VPC)**: Giải phóng Route Tables, Internet Gateway, Subnets và xóa VPC `ResumeMatching-VPC`.
6. **Lưu trữ S3**: Truy cập S3, xóa rỗng (Empty) toàn bộ đối tượng trong bucket `resume-matching-storage-...` và xóa bucket.
7. **Secrets Manager & IAM**: Xóa Secrets lưu trữ trên AWS Secrets Manager và các IAM Roles/Policies liên quan.

---

#### 2. Dự tính Chi phí Triển khai Hệ thống (Cost Breakdown)

##### 2.1. Phương pháp và Cơ sở Tính toán
* **Công cụ tính toán:** AWS Pricing Calculator (Cơ sở dữ liệu giá chính thức của Amazon Web Services).
* **Khu vực triển khai (Region):** US East (N. Virginia) – `us-east-1`.
* **Mô hình giá:** AWS On-Demand Pricing (Không áp dụng Reserved Instances hoặc Savings Plans).
* **Thời gian vận hành:** 730 giờ/tháng (Vận hành liên tục 24/7).
* **Đặc tính lưu lượng:** Hệ thống phục vụ thử nghiệm nghiệm thu đồ án, lưu lượng truy cập mức cơ bản (Low Traffic).

##### 2.2. Bảng Thống kê Chi phí Chi tiết theo Dịch vụ AWS

| STT | AWS Service | Configuration | Quantity | Estimated Monthly Cost (USD) | Notes | Total (USD) |
| :---: | :--- | :--- | :---: | :---: | :--- | :---: |
| **1** | **Amazon VPC** | VPC 10.0.0.0/16, 2 Public Subnets, 4 Private Subnets, Internet Gateway | 01 VPC | 0.00 | Dịch vụ khởi tạo mạng ảo miễn phí | **0.00** |
| **2** | **Security Group** | Tường lửa ảo (ALB-SG, Backend-SG, Worker-SG, RDS-SG) | 04 SGs | 0.00 | Quản lý quy tắc Inbound/Outbound miễn phí | **0.00** |
| **3** | **NAT Gateway** | Managed NAT Gateway ($0.045/giờ/gateway + $0.045/GB data processed) | 02 Gateways | 65.75 | 1,460 giờ chạy On-Demand + ~1 GB Data Processing | **65.75** |
| **4** | **Amazon EC2** | `t3.micro` Linux (2 vCPU, 1 GiB RAM), On-Demand ($0.0104/giờ) | 03 Instances | 22.78 | 01 Backend Server + 02 EC2 trong Auto Scaling Group | **22.78** |
| **5** | **Amazon EBS** | `gp3` General Purpose SSD Storage, dung lượng 30 GB/instance | 03 Volumes (90 GB) | 7.20 | Đơn giá $0.08/GB-tháng x 90 GB | **7.20** |
| **6** | **AMI & Launch Template** | Mẫu cấu hình khởi tạo máy chủ & Amazon Machine Image | 01 LT, 01 AMI | 0.00 | Không tính phí lưu trữ cấu hình mẫu | **0.00** |
| **7** | **Auto Scaling Group** | Tự động co giãn theo tải (Min: 2, Max: 4, Desired: 2) | 01 ASG | 0.00 | Dịch vụ quản trị Auto Scaling miễn phí | **0.00** |
| **8** | **Application Load Balancer** | Internet-facing ALB, Multi-AZ ($0.0225/giờ + LCU) | 01 ALB | 16.44 | 730 giờ vận hành + < 1 LCU lưu lượng | **16.44** |
| **9** | **Target Group** | Instance-type Target Group (HTTP Port 8080) | 01 Target Group | 0.00 | Định tuyến tải miễn phí | **0.00** |
| **10** | **Amazon RDS PostgreSQL** | Single-AZ `db.t3.micro` ($0.018/giờ) + 20 GB `gp3` Storage ($0.08/GB) | 01 DB Instance | 14.74 | $13.14 (Compute) + $1.60 (Storage) | **14.74** |
| **11** | **Amazon S3** | S3 Standard Storage (~5 GB dữ liệu CV/JD, $0.023/GB) | 01 Bucket | 0.12 | Lưu trữ hồ sơ ứng viên & yêu cầu công việc | **0.12** |
| **12** | **Amazon SQS & DLQ** | Standard Queue & Dead Letter Queue (< 1.000 requests/tháng) | 02 SQS Queues | 0.00 | Miễn phí thuộc định mức AWS Free Tier (1M req/tháng) | **0.00** |
| **13** | **AWS Secrets Manager** | Secret lưu trữ DB Credentials, Auth Keys & OpenAI API Key | 01 Secret | 0.40 | Chi phí cố định $0.40/secret/tháng | **0.40** |
| **14** | **Amazon Cognito** | User Pool quản lý định danh ứng viên (< 50.000 MAU) | 01 User Pool | 0.00 | Miễn phí vĩnh viễn cho dưới 50.000 MAU | **0.00** |
| **15** | **AWS Systems Manager** | Session Manager kết nối Shell quản trị an toàn vào EC2 | 01 Service | 0.00 | Miễn phí truy cập quản trị hệ thống | **0.00** |
| **16** | **Amazon CloudWatch** | Basic Metrics (chu kỳ 5 phút) + Monitoring Logs cơ bản | 01 Dashboard | 0.00 | Nằm trong gói giám sát cơ bản miễn phí | **0.00** |
| **TỔNG CỘNG** | | | | | | **127.43 USD** |

##### 2.3. Phân tích và Đánh giá Chi phí Hạ tầng

1. **Tổng Chi phí Vận hành:**
   * Tổng chi phí dự toán duy trì hạ tầng hệ thống Resume Fit là **127.43 USD / tháng** (tương đương khoảng **3.200.000 VNĐ / tháng**).

2. **Phân tích Cơ cấu Chi phí (Cost Structure Analysis):**
   * **Dịch vụ chiếm chi phí cao nhất:** **NAT Gateway** với chi phí **65.75 USD / tháng**, chiếm **51.6%** tổng chi phí toàn hệ thống. Mặc dù lưu lượng dữ liệu truyền qua rất thấp, phí duy trì cố định theo giờ của 02 NAT Gateways ($0.045/giờ x 2) là nguyên nhân chính khiến chi phí tăng cao.
   * **Cụm Tính toán (Compute - EC2 & EBS):** Tổng chi phí cho 3 máy chủ `t3.micro` và 90 GB EBS `gp3` là **29.98 USD / tháng** (chiếm **23.5%**).
   * **Cân bằng tải (ALB):** Chi phí cố định duy trì ALB là **16.44 USD / tháng** (chiếm **12.9%**).
   * **Cơ sở dữ liệu (RDS PostgreSQL):** Chi phí duy trì RDS Single-AZ `db.t3.micro` là **14.74 USD / tháng** (chiếm **11.6%**).

3. **Đánh giá Khả năng Khả thi với Hạn mức AWS Credits 200 USD:**
   * Ngân sách cấp phát **200 USD AWS Credits** hoàn toàn **ĐỦ ĐIỀU KIỆN** để duy trì toàn bộ hạ tầng thực tế hoạt động liên tục (24/7) trong thời gian **1.5 tháng (khoảng 47 ngày)**.
   * Trong kịch bản kiểm thử thực tế phục vụ báo cáo đồ án (chỉ bật hạ tầng trong giờ làm việc hoặc khoảng 8-10 giờ/ngày), hạn mức 200 USD hoàn toàn có thể kéo dài thời gian vận hành từ **3 đến 4 tháng**.

##### 2.4. Đề xuất Giải pháp Tối ưu Chi phí (Cost Optimization Strategies)
Giữ nguyên toàn bộ kiến trúc 3-Tier hiện tại nhưng giảm thiểu chi phí phát sinh:

* **Tối ưu NAT Gateway trong môi trường Dev/Test:** Chuyển đổi từ 02 NAT Gateways xuống 01 NAT Gateway duy nhất tại `Public Subnet A` (trỏ route table của `Private Subnet B` sang NAT Gateway A). Giải pháp này giúp tiết kiệm ngay **32.88 USD / tháng** mà không làm thay đổi logic ứng dụng.
* **Tự động hóa Lịch trình Vận hành (Auto Stop/Start):** Sử dụng AWS EventBridge để tự động dừng (Stop) các instance EC2 và RDS vào buổi tối/cuối tuần khi không có lịch demo đồ án, giúp giảm chi phí tính toán xuống 60% (tiết kiệm thêm **~25.00 USD / tháng**).
* **Thiết lập Thời hạn Lưu trữ Logs (CloudWatch Log Retention):** Giới hạn thời gian lưu giữ log của CloudWatch là 7 ngày thay vì mặc định `Never Expire` để tránh phát sinh chi phí lưu trữ log theo thời gian.
