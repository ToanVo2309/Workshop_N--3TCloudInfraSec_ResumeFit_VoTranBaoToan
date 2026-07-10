---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
# SYSTEM MONITORING ON AWS: STREAMING CLOUDWATCH METRICS TO OPENTELEMETRY COLLECTOR IN VPC USING LAMBDA

Managing observability for large-scale cloud systems has always been a challenging problem, especially when businesses want to balance cost, flexibility, and security. Although OpenTelemetry is gradually becoming the standard to help organizations avoid vendor lock-in, they face a major technical hurdle: how to stream metrics from AWS CloudWatch directly into strict network-isolated internal collectors in the VPC? To solve this, a solution using AWS Lambda acting as a data transit station from CloudWatch Metric Streams to the internal network has proven to be highly effective, ensuring the data stream is always transmitted securely and immediately.

### HERE ARE THE KEY HIGHLIGHTS OF THIS PUSH-BASED OBSERVABILITY SOLUTION:
* **Shift from Pull to Push model:** Using tools like Prometheus to constantly pull/poll data causes API throttling, loss of metrics, and high costs. The push-based model with CloudWatch Metric Streams completely resolves this, enabling event-driven data transmission with sub-minute latency for real-time alerting.
* **Overcoming the limits of Amazon Data Firehose:** Although Firehose supports pushing data to HTTP endpoints, they must be public. To route data to a private subnet, AWS uses a Lambda function (Lambda Transform Function) as a bridge. Firehose aggregates data and invokes Lambda, which then securely pushes metrics via an NLB deep into the VPC.
* **OpenTelemetry Collector is the heart of the system:** Running on Amazon EC2 instances inside the VPC, the Collector acts as a processing hub with 3 flexible components: Receivers (accepting data), Processors (filtering, enriching, masking sensitive data), and Exporters (exporting data to various destinations like Grafana, AWS X-Ray, or Amazon OpenSearch).
* **Scalability and safe backup:** By using a Network Load Balancer to distribute TCP traffic to EC2 instances, the system can easily scale horizontally. Additionally, an Amazon S3 bucket is configured as a backup destination for Firehose (however, no storage cost is incurred if Lambda successfully pushes the data).
* **Cost optimization and eliminating Vendor Lock-in:** Using OpenTelemetry (completely free under Apache 2.0 license) helps businesses eliminate the license cost of third-party software. Its standardization allows operations teams to freely change backend monitoring platforms in the future without rebuilding the data collection pipeline.

In general, the clever combination of AWS services like Lambda, Firehose, and Network Load Balancer creates a perfect bridge, closing the gap between the public cloud services and the isolated internal network. This architecture not only solves the latency or limitation issues of traditional APIs but also empowers technical teams to the fullest. By establishing an intelligent data transmission pipeline, businesses can freely build a powerful, independent, budget-optimized monitoring ecosystem that is always ready to scale in the future without vendor lock-in risks.

Building a monitoring system is not hard; the challenge is to make it secure, low-cost, and vendor-neutral. How do you evaluate this push-based architecture with Lambda and OpenTelemetry? If you are running a system, is your biggest obstacle security (sending metrics securely to a private VPC) or infrastructure cost optimization? Let's discuss!

![Architecture Diagram](/images/blog1_arch.png)

* [Facebook Post Link](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2173544653410495/?rdid=CUzsR7GSYpgaIwjW)
* [AWS Implementation Guide](https://aws.amazon.com/vi/blogs/architecture/streaming-cloudwatch-metrics-to-vpc-based-opentelemetry-collectors-using-lambda/)