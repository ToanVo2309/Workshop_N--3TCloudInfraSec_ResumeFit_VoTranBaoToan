---
title: "Validate Auto Scaling Group Functionality"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.9.1 </b> "
---
### 5.9.1 Validate Auto Scaling Group Functionality

#### Implementation Steps:

1. Go to the **EC2 Console**, navigate to **Instances**.
2. Observe that the system automatically initializes new EC2 instances prefixed with `ResumeMatching-ASG-Instance` distributed evenly across Availability Zones.
   ![ASG Spawning EC2](/img/ASG_tao_them_EC2.jpg)
3. Old instances may show `Terminated` state. This demonstrates that the ASG is functioning correctly: automatically terminating unhealthy/old hosts and spinning up new ones based on configuration changes.
   ![ASG New EC2](/img/ASG_tao_EC2_moi_sau%20khi_cap_nhat_AMI.jpg)
