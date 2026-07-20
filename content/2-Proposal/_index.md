---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# AI Resume Matching & Interview Preparation Platform

![Architecture Diagram](/images/2-Proposal/architecture.png)

## 1. Project Overview

- **Objective:** Web application for matching Candidate Resumes (CVs) with Job Descriptions (JDs) built on a standard AWS 3-Tier architecture.
- **AI Processing:** EC2 Cluster (Backend + Worker) handles CV & JD analysis by calling OpenAI APIs over the Internet to optimize token consumption and minimize operational costs.

---

## 2. Cloud Infrastructure Architecture (AWS)

### 2.1. Edge & Global Layer
- Content Delivery Network (CloudFront), WAF firewall, and authentication services are planned (*Planned but not deployed - AWS account verification required*) and not currently active production services.
- Amazon S3 (Amazon Simple Storage Service) is utilized for general storage.
- Users interact via Internet Gateway (1) or upload directly via Pre-signed URLs to dedicated S3 storage (S3 CV/JD Storage) (5).

### 2.2. Network & Load Balancing (Inbound)
- VPC `10.0.0.0/16` serves as the core network foundation.
- Internet Gateway (IGW) acts as the single entry/exit gateway for both Inbound and Outbound traffic (via NAT Gateways).
- Application Load Balancer (ALB) spans across Availability Zones, receiving incoming traffic from IGW and distributing it to the Auto Scaling Group.

### 2.3. Application Tier
- EC2 Cluster (Backend + Worker) is deployed inside isolated Private App Subnets (`Private App Subnet A` & `Private App Subnet B`), spanning 2 Availability Zones (`AZ A` & `AZ B`), managed by an Auto Scaling Group (ASG) for dynamic scaling.
- **Internal Communication:** EC2 (AZ A) connects to S3 storage and SQS (6), backed by a Dead Letter Queue (DLQ).
- **OpenAI API Traffic (AZ B):** Initiated from EC2 (AZ B), passing outbound through the NAT Gateway in Public Subnet B to reach the Internet Gateway.

### 2.4. Outbound & Internal Network
- Dual NAT Gateways deployed in `Public Subnet A` and `Public Subnet B` ensure High Availability (HA) for outbound traffic from Private Subnets.
- SQS and S3 communications route over the network without VPC Endpoints.

### 2.5. Database Tier
- Powered by Amazon RDS PostgreSQL with Multi-AZ deployment.
- Protected by a dedicated Security Group across two Private DB Subnets (`Private DB Subnet A` & `Private DB Subnet B`).
- RDS Primary (Master) resides in AZ A, while RDS Standby Replica in AZ B maintains continuous data synchronization.
- **Connection Flow:** EC2 in AZ A connects directly to RDS Primary (7). EC2 in AZ B connects to RDS Standby Replica via RDS Endpoints.

### 2.6. Management & Monitoring
- A Regional Security & Management suite comprising AWS Systems Manager, Amazon CloudWatch (logs), and AWS Secrets Manager (API Key).

### 2.7. Deployment
- Source code is hosted on GitHub (Manual Deployment). Automated pipelines (AWS CodeBuild/CodePipeline) are not utilized in the current architecture.