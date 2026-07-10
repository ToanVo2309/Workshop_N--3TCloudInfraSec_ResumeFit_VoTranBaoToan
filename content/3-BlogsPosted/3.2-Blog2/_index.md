---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---
# Hands-on Experience: Building an AI Gateway to Manage Amazon Bedrock with API Gateway

Hi everyone. Recently, while working on AWS infrastructure labs—from configuring networks and troubleshooting security with Secrets Manager in Cloud9, to designing system monitoring frameworks integrating Machine Learning with Prometheus—I stumbled upon a rather tough problem: How to manage access control and monitor costs when multiple teams start sharing Large Language Models (LLMs) on Amazon Bedrock?

In practice, when building Generative AI applications, you cannot simply hand out the Bedrock API key for everyone to call directly. Costs would skyrocket, and user isolation (tenant isolation) boundaries would be virtually non-existent. After struggling for a while, I found an excellent reference pattern from Dynatrace and decided to test it. Today, I'll share my experience designing this "AI Gateway" from a hands-on perspective.

### Overall Architecture - Lightweight but Powerful
Instead of having clients access Bedrock directly, we set up a shield using Amazon API Gateway as the central entry point. The entire flow is broken down as follows:

* **Route 53 (Optional but recommended):** Instead of using the default long AWS endpoint, Route 53 maps a custom domain to make it look clean and fit enterprise standards.
* **API Gateway (Main Entry):** Here, we configure rate-limiting rules to prevent spam and allocate quotas to prevent budget overruns. The key benefit is that it supports response streaming, so when the application needs to stream text from the LLM word-by-word in real time, everything runs extremely smoothly.
* **Lambda Authorizer (Security Checkpoint):** Clients calling the API cannot come empty-handed. We configure a Lambda function to validate JWT tokens. A valid token is required to proceed.
* **Lambda Integration (The Heart of the System):** This is my favorite part. This Lambda function acts as a diligent courier. It captures the user's original request (headers, body, parameters), automatically signs it with AWS Signature Version 4 (SigV4), and forwards it to the correct Amazon Bedrock destination.

### Why Do I Highly Value This Pattern?
During practical implementation, this model solves two core issues that infrastructure engineers care about deeply:

1. **Transparent to Client:** I frequently test code locally and use the Boto3 library extensively. The beauty of this gateway is that when calling the API, the client-side code requires almost no modification. The external application acts as if it is communicating directly with Bedrock, while everything is secretly inspected and audited behind the scenes.
2. **Future-proof Design:** Anyone working on Cloud knows that AWS updates new Bedrock features constantly. If the gateway had to hardcode every single API endpoint, we would have to modify the code every time a new model is released. Thanks to the Lambda Integration design, which only handles "packaging and signing" without interfering with the API structure, if Bedrock launches a new model or updates Knowledge Bases tomorrow, our system will continue to run stably without requiring maintenance code.

### Conclusion
Since I work on monitoring and data visualization systems (like Grafana or Zabbix), consolidating all AI traffic flows into a single API Gateway makes it extremely easy to plug in monitoring tools to track system health and individual project costs.

Leveraging Serverless services as the management layer for AI not only enhances security but also optimizes operations significantly. If you are building infrastructure for GenAI applications on AWS, this AI Gateway model is definitely a valuable piece to incorporate into your system.

![Architecture Diagram](/images/blog2_arch.png)

* [Facebook Post Link](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2179637596134534/?rdid=654DT9MyMTrqQ5kg#)
* [AWS Reference Architecture](https://aws.amazon.com/vi/blogs/architecture/building-an-ai-gateway-to-amazon-bedrock-with-amazon-api-gateway/)