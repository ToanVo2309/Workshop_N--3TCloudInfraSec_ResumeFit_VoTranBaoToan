---
title: "Dọn dẹp tài nguyên"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---
### 5.11. Dọn dẹp tài nguyên & Phân tích chi phí

#### 1. Quy trình Dọn dẹp Tài nguyên

Sau khi hoàn tất quá trình thực hiện bài lab và kiểm thử, để tránh phát sinh thêm chi phí duy trì hạ tầng không cần thiết trên AWS, hãy thực hiện dọn dẹp các tài nguyên theo thứ tự dưới đây:

1. **Auto Scaling Group**: Xóa Auto Scaling Group trước để ngăn chặn tự động khởi tạo lại máy chủ mới. Tiến hành Terminate các instance còn lại.
2. **Cân bằng tải (ALB)**: Xóa Application Load Balancer và Target Group liên quan.
3. **Cơ sở dữ liệu (RDS)**: Xóa PostgreSQL DB Instance. Bỏ chọn tùy chọn tạo final snapshot nếu không muốn lưu giữ dữ liệu. Sau khi database bị xóa, tiến hành xóa DB Subnet Group.
4. **NAT Gateway**: Xóa các NAT Gateways đã tạo. Đợi trạng thái NAT Gateway chuyển hẳn sang `Deleted`, sau đó tiến hành Release các Elastic IP tĩnh.
5. **Hạ tầng Mạng (VPC)**: Giải phóng VPC Endpoints, Route Tables, Internet Gateway, Subnets và cuối cùng là xóa VPC `ResumeMatching-VPC`.
6. **Lưu trữ S3**: Truy cập S3, xóa rỗng (Empty) toàn bộ đối tượng trong bucket `resume-matching-storage-...` và sau đó xóa bucket.
7. **Secrets & IAM**: Xóa các Secrets đã lưu trữ trên Secrets Manager và các IAM Roles/Policies liên quan.

---

#### 2. Báo cáo Phân tích Chi phí Triển khai (AWS Cost Breakdown)

Báo cáo ước tính chi phí duy trì hệ thống **Resume Fit** trên nền tảng AWS được lập bởi **AWS Cloud Solutions Architect**, dựa trên công cụ tính toán chính thức **AWS Pricing Calculator**.

##### 2.1. Giả định và Thông số Tính toán
* **Vùng triển khai (Region):** US East (N. Virginia) – `us-east-1`.
* **Mô hình giá (Pricing Model):** AWS On-Demand Pricing (Không áp dụng Reserved Instance hoặc Savings Plans).
* **Thời gian vận hành:** 730 giờ/tháng (Vận hành liên tục 24/7).
* **Tải lưu lượng (Traffic Load):** Lưu lượng truy cập thấp, phục vụ mục đích kiểm thử demo và đánh giá đồ án tốt nghiệp.

##### 2.2. Bảng Dự toán Chi phí Chi tiết Hàng tháng

| STT | AWS Service | Configuration | Quantity | Estimated Monthly Cost (USD) | Notes | Total (USD) |
| :---: | :--- | :--- | :---: | :---: | :--- | :---: |
| **1** | **Amazon VPC** | Virtual Private Cloud (`10.0.0.0/16`) | 01 | 0.00 | Dịch vụ mạng ảo cơ sở, không tính phí khởi tạo | 0.00 |
| **2** | **Internet Gateway** | Internet Gateway (IGW) kết nối VPC với Internet | 01 | 0.00 | Miễn phí định tuyến Gateway Inbound/Outbound | 0.00 |
| **3** | **Subnets** | 2 Public, 2 Private App, 2 Private DB Subnets | 06 | 0.00 | Cấu hình phân chia dải mạng nội bộ | 0.00 |
| **4** | **NAT Gateway** | Managed NAT Gateway (0.045 USD/giờ + Lưu lượng xử lý) | 02 | 65.70 | 2 NAT x 730h x 0.045 USD/h (Dự phòng HA 2 AZs) | 65.70 |
| **5** | **Security Group** | Tường lửa ảo kiểm soát Inbound/Outbound traffic | 04 | 0.00 | Miễn phí cấu hình quy tắc tường lửa | 0.00 |
| **6** | **Amazon EC2** | `t3.micro` Linux (2 vCPU, 1 GiB RAM, 0.0104 USD/giờ) | 03 | 22.78 | 01 Backend Server + 02 Instance thuộc ASG | 22.78 |
| **7** | **Amazon EBS Storage** | `gp3` SSD Storage (30 GB/instance, 0.08 USD/GB/tháng) | 90 GB | 7.20 | Lưu trữ HĐH Linux và ứng dụng Backend/Worker | 7.20 |
| **8** | **Amazon Machine Image** | Custom AMI (`ResumeMatching-Backend-AMI`) | 01 | 0.00 | Miễn phí quản lý AMI (chỉ tính dung lượng EBS) | 0.00 |
| **9** | **Launch Template & ASG** | Launch Template & Auto Scaling Group | 01 | 0.00 | Dịch vụ tự động mở rộng không tính phí quản lý | 0.00 |
| **10** | **Application Load Balancer** | ALB (0.0225 USD/giờ + LCU usage) | 01 | 16.88 | 730h x 0.0225 USD/h + LCU lưu lượng demo | 16.88 |
| **11** | **Target Group** | Target Group điều hướng HTTP Port 8080 | 01 | 0.00 | Cấu hình kiểm tra sức khỏe máy chủ (Health Check) | 0.00 |
| **12** | **Amazon RDS PostgreSQL** | Single-AZ `db.t3.micro` Instance (0.018 USD/giờ) | 01 | 13.14 | 730h x 0.018 USD/h (Cơ sở dữ liệu PostgreSQL) | 13.14 |
| **13** | **Amazon RDS Storage** | `gp3` Database Storage (20 GB, 0.115 USD/GB/tháng) | 20 GB | 2.30 | Dung lượng lưu trữ dữ liệu quan hệ ứng dụng | 2.30 |
| **14** | **Amazon S3 Standard** | Standard Object Storage (CV/JD, 0.023 USD/GB/tháng) | 5 GB | 0.12 | 5 GB dữ liệu lưu trữ + Request thao tác cơ bản | 0.12 |
| **15** | **Amazon SQS & DLQ** | Standard Queue & Dead Letter Queue | 02 Queues | 0.00 | Thuộc AWS Free Tier (Miễn phí 1 triệu request/tháng) | 0.00 |
| **16** | **AWS Secrets Manager** | Lưu trữ Secret nhạy cảm (0.40 USD/secret/tháng) | 01 Secret | 0.40 | Quản lý API Key OpenAI và DB Credentials | 0.40 |
| **17** | **Amazon Cognito** | User Pool xác thực người dùng (MAU < 50.000) | 01 Pool | 0.00 | Miễn phí cho 50.000 người dùng hoạt động hàng tháng | 0.00 |
| **18** | **AWS Systems Manager** | SSM Session Manager kết nối SSH an toàn | Active | 0.00 | Miễn phí kết nối điều khiển EC2 không mở port 22 | 0.00 |
| **19** | **Amazon CloudWatch** | Basic Monitoring & Log Ingestion (5 GB miễn phí) | Active | 0.00 | Miễn phí chỉ số cơ bản và 5 GB lưu trữ log | 0.00 |
| **TỔNG CỘNG** | | | | | **Tổng chi phí ước tính hàng tháng** | **128.52 USD** |

---

##### 2.3. Tổng Chi phí Triển khai Hàng tháng
Tổng chi phí ước tính để duy trì toàn bộ hạ tầng hệ thống **Resume Fit** vận hành liên tục 24/7 trong một tháng (730 giờ) là **128.52 USD/tháng** (tương đương khoảng **3.213.000 VNĐ/tháng** theo tỷ giá tạm tính 1 USD = 25.000 VNĐ).

##### 2.4. Phân tích Dịch vụ Chiếm Chi phí Cao nhất (Cost Drivers Analysis)
1. **NAT Gateway (65.70 USD - Chiếm 51.1% tổng chi phí):** 
   - Đây là yếu tố chiếm tỷ trọng chi phí lớn nhất trên toàn hệ thống. Việc duy trì 02 NAT Gateway tại 02 Availability Zones (AZ A & AZ B) phục vụ tính sẵn sàng cao (High Availability) phát sinh chi phí duy trì cố định theo giờ (0.045 USD/giờ/NAT Gateway), độc lập với lưu lượng dữ liệu truyền qua.
2. **Cụm tính toán EC2 & Đĩa lưu trữ EBS (29.98 USD - Chiếm 23.3% tổng chi phí):**
   - Chi phí cho 03 máy chủ `t3.micro` vận hành 24/7 chiếm 22.78 USD/tháng và 90 GB ổ đĩa `gp3` SSD gắn kèm chiếm 7.20 USD/tháng.
3. **Application Load Balancer (16.88 USD - Chiếm 13.1% tổng chi phí):**
   - Chi phí duy trì ALB cố định theo giờ để phân phối lưu lượng Inbound từ Internet tới cụm máy chủ trong Private Subnets.
4. **Cơ sở dữ liệu Amazon RDS PostgreSQL (15.44 USD - Chiếm 12.0% tổng chi phí):**
   - Bao gồm chi phí instance `db.t3.micro` (13.14 USD) và 20 GB dung lượng đĩa `gp3` (2.30 USD).

##### 2.5. Đánh giá Khả năng Đáp ứng với Hạn mức AWS Credits (200 USD Credit Evaluation)
* **Kết luận:** Hệ thống **HOÀN TOÀN PHÙ HỢP** và nằm trong tầm kiểm soát của ngân sách **200 USD AWS Credits**.
* **Phân tích chi tiết:**
  - Nếu duy trì hệ thống chạy liên tục 24/7 (phí 128.52 USD/tháng), hạn mức 200 USD Credits cho phép vận hành hệ thống xuyên suốt trong vòng **1.55 tháng** (~46 ngày) mà không phát sinh thêm bất kỳ chi phí thực tế nào.
  - Trong kịch bản thực tế thử nghiệm đồ án (chỉ khởi chạy hệ thống trong thời gian kiểm thử và chấm đồ án, khoảng 8 giờ/ngày và 5 ngày/tuần), chi phí thực tế sẽ giảm xuống chỉ còn khoảng **43.00 USD/tháng**, giúp hạn mức 200 USD Credits duy trì hoạt động đồ án lên tới **4.6 tháng**.

##### 2.6. Đề xuất Giải pháp Tối ưu Chi phí (Cost Optimization Recommendations)
Để tối ưu hóa ngân sách nhưng **tuyệt đối giữ nguyên kiến trúc hệ thống hiện tại**, các giải pháp sau được đề xuất:
1. **Tối ưu hóa NAT Gateway trong môi trường Demo (Tiết kiệm 32.85 USD/tháng):**
   - Trong giai đoạn chấm đồ án, có thể cấu hình gom lại sử dụng **01 NAT Gateway** chung cho cả 2 Private App Subnets thay vì 02 NAT Gateway riêng biệt ở 2 AZs. Giải pháp này giúp cắt giảm ngay 50% chi phí NAT Gateway, đưa tổng chi phí hệ thống xuống còn **95.67 USD/tháng** (tiết kiệm 25.5% tổng chi phí toàn hệ thống).
2. **Áp dụng Lịch trình Tắt/Mở Tự động (Scheduled Auto Start/Stop):**
   - Thiết lập AWS EventBridge kích hoạt Lambda tự động Stop cụm máy chủ EC2 và RDS Instance ngoài giờ đánh giá (từ 22:00 đến 07:00 sáng hôm sau và các ngày cuối tuần). Giải pháp này giúp giảm thêm 60% chi phí tính toán EC2 và RDS.
3. **Giải phóng tài nguyên ngay sau khi nghiệm thu:**
   - Thực hiện đúng quy trình xóa tài nguyên theo thứ tự tại Mục 5.11.1 ngay sau khi hoàn thành buổi bảo vệ đồ án để tránh phát sinh chi phí duy trì duy trì không cần thiết.
