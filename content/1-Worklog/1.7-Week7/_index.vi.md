---
title: "Worklog Tuần 7"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:
* Hiểu nguyên lý hoạt động và ưu điểm của mô hình điện toán không máy chủ với AWS Lambda.
* Triển khai cổng kết nối API Gateway để giao tiếp giữa client và các hàm xử lý Lambda.
* Cấu hình phân quyền IAM và theo dõi dấu vết xử lý log của hàm Lambda qua CloudWatch Logs.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | ------------ | --------------- | -------------- |
| Thứ 2 | Nghiên cứu kiến trúc Lambda, các môi trường runtime, cách định lượng RAM và trigger kích hoạt. | 01/06/2026 | 01/06/2026 | [Video](https://www.youtube.com/watch?v=eOBqlydpXR0) <br> [Tài liệu AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) |
| Thứ 3 | Tìm hiểu cách thức hoạt động của API Gateway (REST API và HTTP API) để định tuyến URL. | 02/06/2026 | 02/06/2026 | [Tài liệu Amazon API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html) |
| Thứ 4 | Viết một đoạn script Python thực hiện tác vụ tự động hóa và tải lên cấu hình thành AWS Lambda. | 03/06/2026 | 03/06/2026 | [Viết hàm Lambda bằng Python](https://docs.aws.amazon.com/lambda/latest/dg/lambda-python.html) |
| Thứ 5 | Tạo API Gateway thiết lập các endpoint HTTP GET/POST để kích hoạt chạy hàm Lambda từ xa. | 04/06/2026 | 04/06/2026 | [Kích hoạt Lambda từ API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/getting-started-with-lambda-integration.html) |
| Thứ 6 | Cấu hình IAM Execution Role cho Lambda và theo dõi kết quả in ra logs qua CloudWatch Logs. | 05/06/2026 | 05/06/2026 | [Phân quyền thực thi IAM cho Lambda](https://docs.aws.amazon.com/lambda/latest/dg/lambda-intro-execution-role.html) |

### Kết quả đạt được tuần 7:
* Xây dựng thành công hệ thống Backend Serverless tự động chạy mã nguồn không cần quản lý máy chủ.
* Định cấu hình API Gateway định tuyến chuẩn các yêu cầu HTTP bên ngoài chuyển tiếp tới microservices.
* Phân quyền bảo mật tối ưu (IAM Role) giúp hàm Lambda chỉ được phép đọc ghi các tài nguyên cần thiết.
* Sử dụng thành thạo CloudWatch Logs để kiểm tra và tối ưu hóa thời gian phản hồi của code.
