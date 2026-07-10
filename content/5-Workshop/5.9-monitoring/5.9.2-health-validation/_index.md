---
title: "Health Status Validation"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.9.2 </b> "
---
### 5.9.2 Health Status Validation

#### Implementation Steps:

1. Go to **Target Groups** under Load Balancing, select your target group.
2. Switch to the **Targets** tab and inspect the **Registered targets** table.
3. Confirm that the `Health status` column displays a green `Healthy` state, verifying that the web container is serving traffic.
   ![Target Group Healthy](/img/Target_group_healthy_check.jpg)
