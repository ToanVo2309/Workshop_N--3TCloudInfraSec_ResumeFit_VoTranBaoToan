---
title: "Cấu hình Secrets Manager"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.6.1 </b> "
---
### 5.6.1 Cấu hình Secrets Manager

#### Các bước thực hiện:

1. Truy cập **AWS Secrets Manager**, tạo secret dạng Key/value có tên `ResumeMatching-Secrets` để lưu trữ thông tin nhạy cảm.
2. Cấu hình các trường như `HOST`, `PORT` (`5432`), `USERNAME`, `PASSWORD` và `OPENAI_API_KEY`.
   ![Create Secret](/img/Tao_Secret.jpg)
