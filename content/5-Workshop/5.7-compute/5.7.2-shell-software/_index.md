---
title: "Shell Access and Software Setup"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.7.2 </b> "
---
### 5.7.2 Shell Access and Software Setup

#### Implementation Steps:

1. Connect to the EC2 instance securely using **Systems Manager Fleet Manager**. Select the running node and click **Start terminal session**.
   ![SSM Session Start](/img/Connect_EC2_backend_bang_Systems_Manager.jpg)
2. Execute command to install **Git**:
   ```bash
   sudo dnf install git
   ```
   ![Install Git](/img/Cai_GIT.jpg)
3. Install and start **Docker** to run containerized application:
   ```bash
   sudo dnf install -y docker
   sudo systemctl enable docker
   sudo systemctl start docker
   ```
   ![Install Docker](/img/Cai_Docker.jpg)
4. Check the status of the Docker daemon:
   ```bash
   sudo systemctl status docker
   ```
   ![Check Docker](/img/Kiem_tra_trang_thai_Docker.jpg)
5. Navigate to `/opt` and clone the application source code from GitHub:
   ```bash
   cd /opt
   sudo git clone http://github.com/thuanthien-tran/resume-fit.git
   sudo chown -R ssm-user /opt/resume-fit
   ```
   ![Clone Repo](/img/Clone_source_len_EC2.jpg)
