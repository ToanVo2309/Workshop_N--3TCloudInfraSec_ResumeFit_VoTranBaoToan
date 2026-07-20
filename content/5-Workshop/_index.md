---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---
# Deploying AI Resume Matching & Interview Preparation Platform on AWS

#### Overview

This lab provides step-by-step guidance on deploying the comprehensive **Resume Fit** system on AWS. Resume Fit is an AI-powered application designed to match Candidate Resumes (CVs) with Job Descriptions (JDs) quickly and transparently, assisting recruitment decisions.

The system is designed following a standard architecture on AWS, ensuring scalability and high availability.

#### 1. Source code and Demo
- **1.1 Resume Fit Demo Link:** [http://resumematching-alb-1223673352.us-east-1.elb.amazonaws.com](http://resumematching-alb-1223673352.us-east-1.elb.amazonaws.com)
- **1.2 Resume Fit Source Code Link:** [https://github.com/thuanthien-tran/resume-fit](https://github.com/thuanthien-tran/resume-fit)

#### 2. AWS Services Used by the Project
The platform leverages core AWS cloud services to ensure high availability and security:
- **Network Isolation (VPC & Security)**: [5.3. Build Virtual Networks](5.3-networking/) & [5.4. Configure Security and IAM Policies](5.4-security/)
- **Storage & Asynchronous Queuing**: [5.5. S3 Storage and SQS Queues Setup](5.5-storage-queue/)
- **Relational Database (PostgreSQL)**: [5.6. RDS PostgreSQL Configuration](5.6-database/)
- **Compute & Auto Scaling**: [5.7. Deploy EC2 Instances](5.7-compute/) & [5.8. Auto Scaling and Load Balancing](5.8-scaling-alb/)
- **Monitoring & Secrets Management**: [5.9. System Observability (Monitoring)](5.9-monitoring/)

#### 3. Development and Deployment
- Source code managed via GitHub and deployed using Docker containers on Amazon EC2:
  - Backend & Worker cluster initialization: [5.7. Deploy EC2 Instances](5.7-compute/)
  - Launch Template, Target Group, and Application Load Balancer (ALB) setup: [5.8. Auto Scaling and Load Balancing](5.8-scaling-alb/)
  - Application verification and testing: [5.10. Verification and Testing](5.10-testing/)

#### 4. Cost and Resource Cleanup
- Implementation cost estimation report (AWS Pricing Calculator) and step-by-step cleanup instructions:
  - Refer to: [5.11. Clean Up Resources and Cost Analysis](5.11-cleanup/)

---

#### Lab Contents

1. [5.1. Introduction](5.1-intro/)
2. [5.2. Prerequisites](5.2-prerequisites/)
3. [5.3. Build Virtual Networks](5.3-networking/)
4. [5.4. Configure Security and IAM Policies](5.4-security/)
5. [5.5. S3 Storage and SQS Queues Setup](5.5-storage-queue/)
6. [5.6. RDS PostgreSQL Configuration](5.6-database/)
7. [5.7. Deploy EC2 Instances](5.7-compute/)
8. [5.8. Auto Scaling and Load Balancing](5.8-scaling-alb/)
9. [5.9. System Observability (Monitoring)](5.9-monitoring/)
10. [5.10. Verification and Testing](5.10-testing/)
11. [5.11. Clean Up Resources and Cost Analysis](5.11-cleanup/)
