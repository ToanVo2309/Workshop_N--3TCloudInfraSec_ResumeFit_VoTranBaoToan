---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
# Một tính năng khá hay của AWS Lake Formation

Gần đây khi tìm hiểu về Data Lake trên AWS, mình đọc được một bài viết khá thú vị từ AWS về Lake Formation nên muốn chia sẻ lại với mọi người.

Nhìn vào mô hình có thể thấy:
* **EMR Spark** đọc/ghi dữ liệu trực tiếp với S3 thông qua IAM Permissions.
* **Lake Formation** quản lý quyền trên các bảng dữ liệu trong Glue Catalog.
* **Athena** truy vấn dữ liệu dựa trên quyền của Lake Formation.

Điều này dẫn đến một tình huống khá phổ biến:
Bạn có thể query dữ liệu bằng Athena bình thường, nhưng khi dùng Spark để đọc trực tiếp file trong S3 lại gặp lỗi `Access Denied`.

Nguyên nhân là vì Athena và Spark đang sử dụng hai cơ chế phân quyền khác nhau:
* **Athena** → Lake Formation
* **Spark đọc file S3** → IAM / S3 Policy

AWS vừa giới thiệu một tính năng mới giúp giải quyết vấn đề này.
Lake Formation giờ đây có thể cấp temporary credentials để Spark truy cập trực tiếp dữ liệu trong S3 dựa trên quyền đã được cấp trong Lake Formation thông qua API:
`GetTemporaryDataLocationCredentials()`

Theo mình, điểm hay nhất của tính năng này là:
* Giảm việc phải quản lý quyền ở nhiều nơi.
* Hạn chế lỗi `Access Denied` do lệch cấu hình.
* Thuận tiện hơn cho các workload Spark, ETL và Machine Learning.
* Dễ theo dõi hoạt động truy cập dữ liệu thông qua CloudTrail.

Một vài lưu ý là tính năng này hiện yêu cầu:
* S3 Location phải được đăng ký với Lake Formation.
* Yêu cầu Amazon EMR 6.15.0+ hoặc 7.1.0+.
* Chưa hỗ trợ Apache Iceberg.
* Chưa hỗ trợ Cross-Region.

Mình thấy đây là một cải tiến khá hữu ích cho các hệ thống Data Lake trên AWS, đặc biệt trong các môi trường sử dụng cả Athena và EMR Spark.

![Sơ đồ kiến trúc](/images/blog3_arch.png)

* [Link bài viết Facebook](https://www.facebook.com/groups/awsstudygroupfcj/posts/2191055074992786/?notif_id=1782041739635661&notif_t=group_post_approved&ref=notif)
* [Tài liệu hướng dẫn AWS](https://aws.amazon.com/vi/blogs/big-data/access-amazon-s3-data-files-directly-using-aws-lake-formation-permissions/?fbclid=IwY2xjawSu8LtleHRuA2FlbQIxMABicmlkETFDd1poRWJtcTNFMEw4bmJKc3J0YwZhcHBfaWQQMjIyMDM5MTc4ODIwMDg5MgABHlfRqurG5Rir4FRt1bIoRDfriCsPR9wuIOYoTnZdypKxZVcIBVgtWsk4A8C9_aem_pW5Px8mN6tGNyQOA7DJaXA)