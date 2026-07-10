---
title: "Week 3 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:
* Understand custom networking with Virtual Private Cloud (VPC).
* Configure Public and Private subnets, routing tables, and internet gateways.
* Enforce security at the network layer using Security Groups and Network ACLs.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | ---------- | --------------- | ------------------ |
| Monday | Study VPC core components: CIDR Blocks, Subnets, Internet Gateways (IGW), and Route Tables. | 04/05/2026 | 04/05/2026 | [Video](https://www.youtube.com/watch?v=jZNv98SyP_c) <br> [Amazon VPC Overview](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html) |
| Tuesday | Understand the role of NAT Gateway/NAT Instance for private subnet outbound internet access. | 05/05/2026 | 05/05/2026 | [NAT Gateway Guide](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) |
| Wednesday | Create a custom VPC, configure Public & Private Subnets, and set up Route Tables. | 06/05/2026 | 06/05/2026 | [Create Custom VPC](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-vpcs.html) |
| Thursday | Study the differences between Security Groups (stateful) and Network ACLs (stateless). | 07/05/2026 | 07/05/2026 | [Security Groups vs NACLs](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Security.html) |
| Friday | Launch EC2 instances in both subnets and verify routing and internet connectivity configurations. | 08/05/2026 | 08/05/2026 | [Troubleshoot EC2 Connection](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/TroubleshootingInstancesConnecting.html) |

### Week 3 Achievements:
* Designed and constructed a custom VPC network skeleton from scratch.
* Understood subnetting design patterns for separating web tiers from database layers.
* Implemented outbound-only internet access for private hosts via NAT Gateways.
* Configured stateful host firewalls (Security Groups) and stateless subnet firewalls (NACLs) correctly.
