---
title: "S3 Bucket Initialization"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.5.1 </b> "
---
### 5.5.1 S3 Bucket Initialization

#### Implementation Steps:

1. Go to **S3**, click **Create bucket** to create a repository for candidate resumes and documentation.
2. Set a globally unique bucket name like `resume-matching-storage-[AWS-ACCOUNT-ID]-us-east-1`.
   ![S3 Creation](/img/Tao_S3.jpg)
3. Create separate storage folders (e.g. `raw/` and `processed/`).
   ![S3 Folders](/img/Create_Folder_S3.jpg)
4. Under the **Permissions** tab, edit **Cross-origin resource sharing (CORS)**. Add JSON configuration allowing `GET`, `PUT`, `POST` methods so that the web frontend can upload files directly to the bucket.
   ![S3 CORS](/img/Bo_sung_CORS_S3.jpg)
