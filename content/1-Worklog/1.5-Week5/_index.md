---
title: "Week 5 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:
* Deploy highly available architectures using Application Load Balancers (ALB).
* Configure Auto Scaling Groups (ASG) to handle traffic elasticity.
* Integrate AWS WAF with ALB to filter malicious traffic.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | ---------- | --------------- | ------------------ |
| Monday | Study Application Load Balancer (ALB) mechanisms, target groups, and health checks. | 18/05/2026 | 18/05/2026 | [Video](https://www.youtube.com/watch?v=Vl03U1jF4gI) <br> [Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html) |
| Tuesday | Learn Auto Scaling Group (ASG) components: launch templates, scaling policies, and cool downs. | 19/05/2026 | 19/05/2026 | [Auto Scaling Concepts](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html) |
| Wednesday | Deploy a load-balanced multi-instance application setup behind an ALB. | 20/05/2026 | 20/05/2026 | [ALB Getting Started](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/application-load-balancer-getting-started.html) |
| Thursday | Configure ASG scaling policies to automatically provision/terminate EC2 instances based on load. | 21/05/2026 | 21/05/2026 | [ASG Scaling Policies](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-scaling-target-tracking.html) |
| Friday | Attach AWS WAF rules to the ALB and perform load testing to verify system resiliency. | 22/05/2026 | 22/05/2026 | [AWS WAF Developer Guide](https://docs.aws.amazon.com/waf/latest/developerguide/waf-chapter.html) |

### Week 5 Achievements:
* Built a resilient multi-AZ web server topology with automatic traffic distribution.
* Configured self-healing capabilities allowing the system to replace unhealthy nodes automatically.
* Established elastic scaling policies responding dynamically to traffic surges.
* Secured the entry point using web application firewall policies to reject unauthorized requests.
