---
title: "Dọn dẹp tài nguyên và Phân tích chi phí"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---
### 5.11. Dọn dẹp tài nguyên và Phân tích chi phí

---

#### 1. Quy trình dọn dẹp tài nguyên AWS

Sau khi hoàn tất quá trình thực hiện bài lab và kiểm thử, để tránh phát sinh thêm chi phí duy trì hạ tầng không cần thiết trên AWS, hãy thực hiện dọn dẹp các tài nguyên theo đúng thứ tự dưới đây:

1. **Auto Scaling Group**: Xóa Auto Scaling Group trước để ngăn chặn hệ thống tự động khởi tạo lại máy chủ mới. Tiến hành Terminate các instance thủ công còn lại.
2. **Cân bằng tải (ALB)**: Xóa Application Load Balancer và Target Group liên quan.
3. **Cơ sở dữ liệu (RDS)**: Xóa PostgreSQL DB Instance. Bỏ chọn tùy chọn tạo final snapshot nếu bạn không muốn lưu giữ dữ liệu. Sau khi database bị xóa, tiến hành xóa DB Subnet Group.
4. **NAT Gateway**: Xóa các NAT Gateways đã tạo. Đợi trạng thái NAT Gateway chuyển hẳn sang `Deleted`, sau đó tiến hành Release các Elastic IP tĩnh.
5. **Hạ tầng Mạng (VPC)**: Giải phóng VPC Endpoints, Route Tables, Internet Gateway, Subnets và cuối cùng là xóa VPC `ResumeMatching-VPC`.
6. **Lưu trữ S3**: Truy cập S3, xóa rỗng (Empty) toàn bộ đối tượng trong bucket `resume-matching-storage-...` và sau đó xóa bucket.
7. **Secrets & IAM**: Xóa các Secrets đã lưu trữ trên Secrets Manager và các IAM Roles/Policies liên quan nếu không có nhu cầu sử dụng tiếp.

---

#### 2. Phân tích chi tiết chi phí vận hành hệ thống (AWS Cost Breakdown Report)

Báo cáo dưới đây được lập bởi **AWS Cloud Solutions Architect** sử dụng công cụ tính toán chính thức **AWS Pricing Calculator** để ước tính chi phí duy trì hệ thống Resume Fit dựa trên kiến trúc 3-Tier thực tế đã triển khai.

##### 2.1. Căn cứ và Điều kiện tính toán
* **Khu vực triển khai (Region):** US East (N. Virginia) – `us-east-1`.
* **Mô hình định giá (Pricing Model):** AWS On-Demand Pricing (Không áp dụng Reserved Instances hoặc Savings Plans).
* **Thời gian vận hành:** 730 giờ/tháng (Chạy liên tục 24/7).
* **Đặc tính lưu lượng:** Phục vụ mục đích nghiên cứu, demo và chấm đồ án tốt nghiệp (Lưu lượng truy cập cực thấp - Low Traffic).

##### 2.2. Bảng dự tính chi phí triển khai hàng tháng (Estimated Monthly Cost Table)

| STT | AWS Service | Configuration | Quantity | Estimated Monthly Cost (USD) | Notes | Total (USD) |
| :---: | :--- | :--- | :---: | :---: | :--- | :---: |
| 1 | **Amazon VPC** | Isolated Virtual Private Cloud (`10.0.0.0/16`) | 1 | 0.00 | Dịch vụ quản lý mạng cơ bản của AWS | **0.000** |
| 2 | **Internet Gateway (IGW)** | Cổng kết nối Internet công cộng cho VPC | 1 | 0.00 | Thành phần định tuyến VPC | **0.000** |
| 3 | **Subnets** | 02 Public, 02 Private App, 02 Private DB Subnets | 6 | 0.00 | Phân chia dải mạng nội bộ VPC | **0.000** |
| 4 | **Security Groups** | Stateful Virtual Firewalls (`ALB`, `App`, `DB`, `Worker`) | 4 | 0.00 | Tường lửa ảo quản lý cổng kết nối | **0.000** |
| 5 | **NAT Gateway** | Managed NAT (`us-east-1`) + 02 Public IPv4 EIPs ($0.005/h/IP) | 2 | 73.045 | $0.045/h x 2 NAT + $0.005/h x 2 EIP x 730h | **73.045** |
| 6 | **Amazon EC2** | `t3.micro` Linux (2 vCPU, 1 GiB RAM), On-Demand | 3 | 22.776 | 01 Backend + 02 ASG Instances ($0.0104/h) | **22.776** |
| 7 | **Amazon EBS Storage** | General Purpose SSD (`gp3`), 30 GB / Volume | 3 | 7.200 | 90 GB Total x $0.08/GB-tháng (3000 IOPS free) | **7.200** |
| 8 | **Amazon AMI** | Amazon Machine Image tùy chỉnh cho Backend | 1 | 0.00 | Lưu bản đóng gói hệ thống (Trong Free Tier) | **0.000** |
| 9 | **Launch Template** | Cấu hình mẫu khởi tạo EC2 cho Auto Scaling | 1 | 0.00 | Công cụ quản lý cấu hình EC2 | **0.000** |
| 10 | **Auto Scaling Group** | Tự động co giãn EC2 theo tải (Desired: 2, Min: 2, Max: 4) | 1 | 0.00 | Dịch vụ điều phối tính toán tự động | **0.000** |
| 11 | **Application Load Balancer** | ALB Internet-facing (`us-east-1`) + 1 LCU min traffic | 1 | 22.265 | $0.0225/h ALB + $0.008/h LCU x 730h | **22.265** |
| 12 | **Target Group** | Target Group kiểm tra Health Check cổng `8080` | 1 | 0.00 | Định tuyến giao thông Load Balancer | **0.000** |
| 13 | **Amazon RDS PostgreSQL** | Instance `db.t3.micro` Single-AZ + 20 GB `gp3` Storage | 1 | 15.440 | DB Instance ($13.14) + Storage ($2.30) | **15.440** |
| 14 | **Amazon S3 Standard** | Storage lưu trữ CV/JD (Standard Tier, `us-east-1`) | 5 GB | 0.120 | $0.023/GB x 5 GB + API Requests thấp | **0.120** |
| 15 | **Amazon SQS** | Standard Queue + Dead Letter Queue (DLQ) | 2 | 0.000 | Trong định mức AWS Free Tier (1M reqs/tháng) | **0.000** |
| 16 | **AWS Secrets Manager** | Lưu trữ bí mật kết nối DB & OpenAI API Key | 1 Secret | 0.400 | Phí quản lý $0.40/secret/tháng | **0.400** |
| 17 | **Amazon Cognito** | Quản lý xác thực người dùng (User Pool) | 1 Pool | 0.000 | Trong định mức AWS Free Tier (< 50,000 MAU) | **0.000** |
| 18 | **AWS Systems Manager** | Session Manager (Truy cập EC2 Terminal an toàn) | 1 | 0.000 | Quản trị kết nối SSH không cần Bastion Host | **0.000** |
| 19 | **Amazon CloudWatch** | Basic Metrics (EC2/ALB) + Basic Logs (< 5 GB) | 1 | 0.500 | Giám sát hiệu năng và lưu vết log cơ bản | **0.500** |
| **TỔNG CỘNG** | | | | | **TỔNG CHI PHÍ ƯỚC TÍNH MỖI THÁNG** | **141.746 USD** |

---

##### 2.3. Tổng chi phí triển khai hàng tháng
* **Tổng chi phí ước tính:** **141.746 USD / tháng** (Tương đương khoảng **3.543.000 VNĐ / tháng** theo tỷ giá quy đổi 25.000 VNĐ/USD).

##### 2.4. Phân tích dịch vụ chiếm chi phí cao nhất
* **NAT Gateway (73.045 USD - Chiếm 51.53% tổng chi phí):** Là thành phần tiêu tốn ngân sách lớn nhất trong hệ thống.
  * *Nguyên nhân:* Hệ thống duy trì 02 NAT Gateway tại 2 Availability Zones (Public Subnet A & B) nhằm đảm bảo tính sẵn sàng cao (High Availability - HA), cho phép các EC2 nằm trong Private App Subnets kết nối ra ngoài Internet gọi API OpenAI và cập nhật phần mềm. Chi phí bị đẩy lên cao do chính sách định giá cố định theo giờ duy trì NAT Gateway ($0.045/h/gateway) kết hợp với chi phí quản lý địa chỉ IPv4 công cộng ($0.005/h/IP).
* **Amazon EC2 (22.776 USD - Chiếm 16.07%):** Chi phí vận hành liên tục 3 instance `t3.micro` On-Demand 24/7.
* **Application Load Balancer (22.265 USD - Chiếm 15.71%):** Chi phí duy trì giờ hoạt động của ALB ($0.0225/h) và 1 LCU tối thiểu.
* **Amazon RDS PostgreSQL (15.440 USD - Chiếm 10.89%):** Chi phí hạ tầng cơ sở dữ liệu `db.t3.micro` Single-AZ kèm 20 GB lưu trữ `gp3`.
* *Các dịch vụ còn lại (EBS, S3, Secrets Manager, CloudWatch):* Chỉ chiếm **5.80%** tổng chi phí toàn hệ thống.

##### 2.5. Đánh giá tính phù hợp với hạn mức AWS Credits (200 USD)
* **Kết luận:** Hạn mức **AWS Credits 200 USD** hoàn toàn **ĐỦ KHẢ NĂNG TRANG TRẢ** cho toàn bộ chi phí triển khai và vận hành dự án trong giai đoạn demo / chấm đồ án tốt nghiệp.
* **Cơ sở đánh giá:**
  1. *Kịch bản vận hành liên tục (24/7 cả tháng):* Nếu duy trì hệ thống chạy 730 giờ liên tục trong 01 tháng, tổng chi phí phát sinh là **141.75 USD**, vẫn dư **58.25 USD** trong hạn mức Credits.
  2. *Kịch bản bảo vệ đồ án thực tế (1 - 2 tuần):* Khi chỉ khởi chạy hạ tầng trong thời gian chấm đồ án thực tế (khoảng 7 - 14 ngày), tổng chi phí phát sinh thực tế chỉ dao động từ **33.00 USD đến 66.00 USD**, giúp tối ưu và tiêu tốn chưa đến **33%** tổng ngân sách 200 USD Credits được cấp.

##### 2.6. Đề xuất các biện pháp tối ưu hóa chi phí (Giữ nguyên kiến trúc)
Để tiết kiệm ngân sách mà hoàn toàn **không làm thay đổi kiến trúc hệ thống 3-Tier**, có thể áp dụng các giải pháp sau:
1. **Tối ưu hóa NAT Gateway (Tiết kiệm 36.53 USD/tháng):**
   * *Giải pháp:* Chuyển đổi từ 02 NAT Gateway xuống **01 NAT Gateway** duy nhất đặt tại Public Subnet A (Giữ nguyên cấu trúc VPC và 6 Subnets hiện tại). Cấu hình Route Table của cả 2 Private App Subnets trỏ lưu lượng Outbound về chung NAT Gateway tại Subnet A.
   * *Hiệu quả:* Chi phí NAT Gateway giảm ngay 50%, từ 73.05 USD xuống còn **36.52 USD/tháng**.
2. **Kế hoạch Tắt/Mở tự động (Schedule Stop/Start):**
   * *Giải pháp:* Thiết lập kịch bản tự động Stop 3 máy chủ EC2 và đưa Desired Capacity của Auto Scaling Group về `0` vào buổi đêm hoặc các ngày không diễn ra chấm đồ án.
   * *Hiệu quả:* Giảm 60 - 70% chi phí máy chủ tính toán EC2 và chi phí LCU của ALB.
3. **Triển khai S3 Gateway Endpoint (Miễn phí):**
   * *Giải pháp:* Tích hợp S3 Gateway Endpoint trực tiếp vào VPC (Dịch vụ hoàn toàn miễn phí).
   * *Hiệu quả:* Giúp toàn bộ lưu lượng tải CV/JD giữa EC2 và S3 đi qua mạng nội bộ AWS thay vì đi qua NAT Gateway, triệt tiêu hoàn toàn chi phí Data Processing của NAT.
4. **Cấu hình CloudWatch Log Retention Period:**
   * *Giải pháp:* Đặt thời gian tự động xóa Log trên CloudWatch là **7 ngày** (thay vì mặc định *Never Expire*).
   * *Hiệu quả:* Tránh tích lũy dung lượng lưu trữ log không cần thiết theo thời gian.
