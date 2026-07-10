---
title: "Khởi tạo S3 Bucket"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.5.1 </b> "
---
### 5.5.1 Khởi tạo S3 Bucket

#### Các bước thực hiện:

1. Chuyển sang dịch vụ **S3**, nhấn **Create bucket** để tạo nơi lưu trữ CV và tài liệu của ứng viên.
2. Đặt tên bucket có dạng duy nhất: `resume-matching-storage-[AWS-ACCOUNT-ID]-us-east-1`.
   ![S3 Creation](/img/Tao_S3.jpg)
3. Tạo các thư mục phục vụ lưu trữ file riêng biệt (ví dụ `raw/` và `processed/`).
   ![S3 Folders](/img/Create_Folder_S3.jpg)
4. Tại tab **Permissions**, tiến hành chỉnh sửa **Cross-origin resource sharing (CORS)**. Thêm nội dung JSON để cấu hình `AllowedMethods` bao gồm: `GET`, `PUT`, `POST` nhằm cho phép ứng dụng web tải file trực tiếp lên bucket.
   ![S3 CORS](/img/Bo_sung_CORS_S3.jpg)
