---
title: "SQS Queue Setup"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.5.2 </b> "
---
### 5.5.2 SQS Queue Setup

Use message queues to decouple resource-heavy AI matching logic from the synchronous web response flow.

#### Implementation Steps:

1. Open **SQS**. Create a Standard queue named `ResumeMatching-DLQ` (Dead Letter Queue) to capture failed messages.
   ![Create DLQ](/img/Tao_queue.jpg)
2. Create the primary queue named `ResumeMatching-Queue`.
   ![Create Main Queue](/img/Tao_main_queue.jpg)
3. Enable **Dead-letter queue** on the primary queue, pointing it to the ARN of `ResumeMatching-DLQ` and setting `Maximum receives` = `3`.
