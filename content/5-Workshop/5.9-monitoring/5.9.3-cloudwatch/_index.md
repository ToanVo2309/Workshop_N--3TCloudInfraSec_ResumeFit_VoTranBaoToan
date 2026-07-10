---
title: "CloudWatch Dashboard Analytics"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.9.3 </b> "
---
### 5.9.3 CloudWatch Dashboard Analytics

#### Implementation Steps:

1. Access **CloudWatch**, and select **Metrics** for performance tracking.
2. **For EC2**: Filter by EC2 Namespace and select `CPUUtilization`. Monitor the CPU spikes during intense AI analysis tasks to establish scaling thresholds.
   ![CloudWatch EC2](/img/CloudWatch_dang_monitor_EC2.jpg)
   ![EC2 CPU Metrics](/img/EC2_Metrics.jpg)
3. **For ALB**: Monitor `RequestCount` and `TargetResponseTime`. Analyzing the correlation between requests spike and response times helps determine overall system responsiveness.
   ![CloudWatch ALB](/img/CloudWatch_monitor_Load_Balancer.jpg)
   ![ALB Metrics](/img/ALB_Metrics.jpg)
