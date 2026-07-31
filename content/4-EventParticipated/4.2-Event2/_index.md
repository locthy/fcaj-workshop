---
title: "Event 2"
date: 2026-07-28
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Summary Report: “Learning AWS Architecture”

### Event Objectives

- Identify the winning team in the Cloud Architect final round
- Introduce cloud architecture patterns and practical design considerations

### Event Day

That day was the final round of an AWS architecture competition. The atmosphere was both formal and exciting, with contestants, judges, and audience members focused on every presentation and answer. The event was structured in multiple stages, beginning with basic questions and progressing to more complex challenges, in order to evaluate participants’ architectural thinking and practical knowledge.

### Question Rounds

- Easy: Initial questions tested foundational AWS knowledge, such as what a VPC is, the differences between public and private subnets, and the role of an Internet Gateway. These questions ensured that all participants shared a common technical baseline.
- Medium: The next round looked deeper at service selection and design decisions, including whether to use EC2 or Lambda for different workloads, how to configure Auto Scaling for variable traffic, and comparing the trade-offs between S3, EBS, and instance store.
- Hard: The challenge round presented real-world architecture problems, such as designing a distributed multi-AZ system for high availability, creating secure IAM configurations based on least privilege, and optimizing costs with Regional NAT Gateway within the AWS Well-Architected Framework.
- Advanced: The final stage required more complex architectural reasoning, including designing event-driven microservices, integrating AI to improve system behavior, and creating recovery plans for when an Availability Zone fails.

### Final Round Experience

The final round was not only about answering correctly, but also about explaining solutions clearly, logically, and persuasively. High-scoring answers were technically accurate and included a strong rationale for why the proposed approach was appropriate for the scenario. Listening to other teams helped me see alternative architectural approaches and reinforced the idea that the best design is often the simplest one that satisfies all requirements.

The competition also tested communication under pressure. Contestants needed to analyze requirements quickly, propose a viable architecture, and explain the trade-offs to the judges. The judges paid particular attention to security, scalability, cost, and operational simplicity when evaluating each response.

### Lessons Learned from the Final Round

- Strong fundamentals are essential. Mastering VPC, subnet design, and IAM makes it possible to tackle more complex architecture problems.
- Good architecture balances complexity and effectiveness. Avoid unnecessary complexity when a simpler solution is easier to operate and maintain.
- Event-driven architecture and serverless are powerful patterns, but they must be applied in the right business context.
- Designing for failure is critical. Building recovery plans for AZ-level disruptions is a sign of a well-architected system.

### Results and Photos

![Winning team receiving the award](/images/4-Events/4.2-Event2/workshop-2.1.jpg)
*The winning team receives the trophy and certificate during the final round.*

![Speakers presenting cloud architecture](/images/4-Events/4.2-Event2/workshop-2.2.jpg)
*The speakers presenting AWS cloud architecture models, complete with diagrams and expert explanations.*

This final round helped me strengthen my AWS architecture knowledge, practice problem solving across increasing difficulty levels, and improve my ability to present architecture decisions in a clear, convincing way. It also highlighted the difference between theoretical understanding and real-world application under time pressure.
