---
title: "Khởi tạo SQS Queues"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.5.2 </b> "
---
### 5.5.2 Khởi tạo SQS Queues

Sử dụng hàng đợi để tách biệt luồng xử lý AI nặng nề ra khỏi luồng phản hồi web chính, tăng trải nghiệm người dùng.

#### Các bước thực hiện:

1. Chuyển đến giao diện **SQS**. Tạo một hàng đợi Standard có tên `ResumeMatching-DLQ` (Dead Letter Queue) dùng để hứng các message bị lỗi trong quá trình xử lý.
   ![Create DLQ](/img/Tao_queue.jpg)
2. Khởi tạo hàng đợi chính mang tên `ResumeMatching-Queue`.
   ![Create Main Queue](/img/Tao_main_queue.jpg)
3. Bật tính năng **Dead-letter queue** trên hàng đợi chính, trỏ đến ARN của `ResumeMatching-DLQ` và thiết lập `Maximum receives` = `3`.
