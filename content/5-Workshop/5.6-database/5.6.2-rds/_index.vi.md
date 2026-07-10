---
title: "Khởi tạo RDS PostgreSQL"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.6.2 </b> "
---
### 5.6.2 Khởi tạo RDS PostgreSQL

#### Các bước thực hiện:

1. Truy cập giao diện **RDS**, chọn mục **Subnet groups** và tạo một subnet group tên `resumematching-dbsubnetgroup` trỏ vào VPC và gom 2 subnet `Private-DB-A`, `Private-DB-B` lại với nhau.
   ![DB Subnet Group](/img/Tao_DB_Subnet_Group.jpg)
2. Tiến hành khởi tạo Database (DB identifier: `resume-matching-db`) với Engine là **PostgreSQL** và instance class là `db.t3.micro`.
   ![Create RDS DB](/img/Tao_RDS_database.jpg)
3. Sau khi tạo thành công, copy Endpoint của Database vừa khởi tạo và quay lại Secrets Manager để dán cập nhật vào khóa `HOST`.
   ![Update Secret Host](/img/Cap_nhat_Secrets_manager.jpg)
