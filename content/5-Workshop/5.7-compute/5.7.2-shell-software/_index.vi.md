---
title: "Kết nối và Cài đặt Phần mềm"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.7.2 </b> "
---
### 5.7.2 Kết nối và Cài đặt Phần mềm

#### Các bước thực hiện:

1. Truy cập EC2 từ xa an toàn bằng **Systems Manager Fleet Manager**. Chọn Managed node đang Running và nhấn **Start terminal session**.
   ![SSM Session Start](/img/Connect_EC2_backend_bang_Systems_Manager.jpg)
2. Thực thi lệnh cài đặt **Git** để kéo mã nguồn:
   ```bash
   sudo dnf install git
   ```
   ![Install Git](/img/Cai_GIT.jpg)
3. Tiến hành cài đặt và khởi động **Docker** để chạy ứng dụng dạng container:
   ```bash
   sudo dnf install -y docker
   sudo systemctl enable docker
   sudo systemctl start docker
   ```
   ![Install Docker](/img/Cai_Docker.jpg)
4. Kiểm tra trạng thái hoạt động của Docker daemon:
   ```bash
   sudo systemctl status docker
   ```
   ![Check Docker](/img/Kiem_tra_trang_thai_Docker.jpg)
5. Điều hướng tới thư mục `/opt` và tải source code ứng dụng từ GitHub:
   ```bash
   cd /opt
   sudo git clone http://github.com/thuanthien-tran/resume-fit.git
   sudo chown -R ssm-user /opt/resume-fit
   ```
   ![Clone Repo](/img/Clone_source_len_EC2.jpg)
