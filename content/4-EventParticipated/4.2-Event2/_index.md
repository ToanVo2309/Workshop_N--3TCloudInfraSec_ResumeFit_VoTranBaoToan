---
title: "Event 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---
# Summary Report: FCAJ Community Day

### Event Objectives
* **Program Objectives:** Not just to listen to seminars, but a place to connect, exchange, and inspire each other (who knows, you might meet a new partner or friend).
* **Main Message:** Revolving around topics from AI and Cloud to real stories summarized from experts' experience. Discussing prompt optimization, AWS technologies (like CloudFront), the Hackathon journey, and enterprise-grade AI architecture design.
* **Value to Attendees:** Help attendees understand how the job market is changing under the impact of AI, how to build a foundation to avoid being discarded, and equip them with practical problem-solving mindsets for enterprises.

### Speakers
* **Quynh Mai** – Role: MC.
* **Nguyen Gia Hưng** – Head of Solution Architect (AWS Vietnam), Founder of FCAJ.
* **Tinh** – Platform Engineer (Gotam X).
* **Hai Anh** – Presenter (Pacific Vietnam, presented at AWS Singapore Summit & Silicon Valley).
* **Thịnh** – DevOps Engineer (UTM Group, Developers team).
* **Đức** – Specialist in LLM Optimization (Large Language Model Optimization).
* **Vy** – System Engineer (VPBank).

### Key Highlights
* **Problem Overview:** AI makes software creation cheaper, so the demand for software will increase dramatically, creating many new jobs in operation (Platform engineering) and debugging (fixing AI-generated code). Another issue is that generating code using AI without context creates messy, low-quality code (LLM hallucinations).
* **Solutions Introduced:**
  * Need to establish clear context (Context/System Prompt) when using AI: Goal, Persona, Format instead of asking generic questions.
  * Use Multi-Agent Systems to solve complex problems (such as startup credit analysis) instead of cramming everything into a single AI model.
* **Technologies/Services/Tools:**
  * **AWS:** CloudFront (Flat-rate pricing, content compression, DDoS protection), AWS Bedrock, EC2, Lambda, VPC.
  * **AI/LLM:** Amazon Agent platform, Obsidian (to build a Second Brain), MCP (Model Context Protocol).
  * **Other:** Terraform (Infrastructure as Code).
* **Demo or Case Study:**
  * *UTM Morpo Project:* Demo tool using 3 AI agents to generate HTML/UI from images, allowing users to drag/drop and edit directly on the interface during the Hackathon.
  * *LLM Parameter Demo:* Running a comparison of Temperature = 0 on AWS Bedrock vs. Local to prove that on the Cloud, the AI's answers still vary due to Inference Optimization.
* **Key Points:** In enterprise environments, security compliance and risk assessment (Guardrails, Security, Audit) are critical—more important than how many AI tools you plug in.

### Key Takeaways
* **Mindset and Methods:** LLM is a "Probabilistic engine", so do not assume it will always return the exact same result even with Temperature = 0. Do not let AI run completely on "auto-pilot"; always keep a human in the loop.
* **Technical Knowledge:** Understand how CloudFront optimizes cost through flat-rate packages to avoid "bill shocks" from traffic spikes or DDoS attacks.
* **Best Practices:** Avoid the "Internet puller" syndrome (copying tools or code found online straight into projects without understanding the context).
* **Real-World Experience:** In Hackathons, having too many ideas (over-generation) wastes time. You must limit the scope and focus on solving one core problem (such as enhancing the editing experience) to complete it in 36 hours.

### Applying to Work
* **Applying to Current Projects:** Design AI systems according to Multi-agent standards: assign specific jobs to specialized agents (e.g., Financial Analysis Agent, Market Research Agent). Build mTLS and VPC Origin to secure resources.
* **Technologies to Experiment with:** Use Terraform for Infrastructure as Code (IaC) to manage versions easily. Test AWS CloudFront edge protection features (geo-blocking, bot protection).
* **Ideas to Improve Workflow:** Instead of loading data manually, use AI Agents integrated with tools (like MCP connecting Excel) to automatically generate analytics dashboards or summarize meeting notes.

### Event Experience
* **Learning from Speakers:** Realize that in the workplace, employers don't just ask for demos; they ask about actual "Products" and business use cases.
* **Hands-on Exposure:** Watching live demos of a 36-hour app build and visual comparisons of LLM running locally vs. on the cloud.
* **Networking and Connection:** Encouraging self-confidence and standing up to present (from students to speakers) because competition in the job market is extremely fierce.
* **Most Impressive Part:** A strong warning about copying ChatGPT code directly into enterprise systems (destroys coding standards, leaks security).

### Lessons Learned
* **Most Important Knowledge:** Foundations, university degrees, and basic Software Engineering skills are still mandatory. AI is just a plus, it cannot replace core software engineering skills (such as knowing how to decode/encode passwords securely).
* **Real Experience:** To convince top executives to fund AI projects (e.g., 1 billion VND), you must show the ROI (Return on Investment) and actual savings numbers—"Numbers speak louder than words".
* **Next Steps:** Dive deeper into AI Mindset and AI Adoption. Always remember the system building rule: Not only must it run, but it "must run securely, reliably, and serve the users". Read official documentation when configuring AI parameters instead of listening to online rumors.

### Some event photos
![Event Photo 1](/images/event2_1.png)

> Overall, the event not only provided technical knowledge but also helped me reshape my thinking about application design, system modernization, and cross-team collaboration.
