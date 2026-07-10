---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
# A Very Cool Feature of AWS Lake Formation

Recently while researching Data Lakes on AWS, I read a very interesting article from AWS about Lake Formation and wanted to share it with everyone.

Looking at the diagram, we can see:
* **EMR Spark** reads/writes data directly to S3 via IAM Permissions.
* **Lake Formation** manages permissions on data tables in the Glue Catalog.
* **Athena** queries data based on Lake Formation permissions.

This leads to a fairly common situation:
You can query data using Athena normally, but when using Spark to read files directly in S3, you get an `Access Denied` error.

The reason is that Athena and Spark are using two different authorization mechanisms:
* **Athena** → Lake Formation
* **Spark S3 file reading** → IAM / S3 Policy

AWS has recently introduced a new feature to solve this issue.
Lake Formation can now grant temporary credentials for Spark to access S3 data directly based on permissions already granted in Lake Formation via the API:
`GetTemporaryDataLocationCredentials()`

In my opinion, the best points of this feature are:
* Reduces the need to manage permissions in multiple places.
* Minimizes `Access Denied` errors caused by configuration discrepancies.
* More convenient for Spark, ETL, and Machine Learning workloads.
* Easily track data access activity through CloudTrail.

A few notes: currently this feature requires:
* The S3 Location must be registered with Lake Formation.
* Requires Amazon EMR 6.15.0+ or 7.1.0+.
* Apache Iceberg is not yet supported.
* Cross-Region is not yet supported.

I think this is a very useful improvement for Data Lake systems on AWS, especially in environments using both Athena and EMR Spark.

![Architecture Diagram](/images/blog3_arch.png)

* [Facebook Post Link](https://www.facebook.com/groups/awsstudygroupfcj/posts/2191055074992786/?notif_id=1782041739635661&notif_t=group_post_approved&ref=notif)
* [AWS Reference Blog](https://aws.amazon.com/vi/blogs/big-data/access-amazon-s3-data-files-directly-using-aws-lake-formation-permissions/?fbclid=IwY2xjawSu8LtleHRuA2FlbQIxMABicmlkETFDd1poRWJtcTNFMEw4bmJKc3J0YwZhcHBfaWQQMjIyMDM5MTc4ODIwMDg5MgABHlfRqurG5Rir4FRt1bIoRDfriCsPR9wuIOYoTnZdypKxZVcIBVgtWsk4A8C9_aem_pW5Px8mN6tGNyQOA7DJaXA)