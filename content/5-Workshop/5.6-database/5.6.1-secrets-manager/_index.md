---
title: "Secrets Manager Configuration"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.6.1 </b> "
---
### 5.6.1 Secrets Manager Configuration

#### Implementation Steps:

1. Open **AWS Secrets Manager**, create a Key/value secret named `ResumeMatching-Secrets` to secure database credentials and API keys.
2. Configure parameters: `HOST`, `PORT` (`5432`), `USERNAME`, `PASSWORD`, and `OPENAI_API_KEY`.
   ![Create Secret](/img/Tao_Secret.jpg)
