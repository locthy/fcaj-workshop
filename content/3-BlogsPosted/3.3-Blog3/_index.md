---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
# WHAT IS AMAZON EVENTBRIDGE? BUILDING EVENT-DRIVEN APPS ON AWS

Amazon EventBridge is a serverless service that connects application components through event creation and processing. It forms the foundation of event-driven architecture — a design style that favors loose coupling, where services communicate by emitting and responding to events instead of calling each other directly. This makes systems more flexible and easier to scale.

![VPC Architecture](/images/5-Workshop/5.3-vpc/vpc_archi2.png)

### Key points to know

- EventBridge provides two main mechanisms for event processing and routing: Event buses and Pipes.
- The event bus acts as a router, receiving events from multiple sources (custom apps, AWS services, and third-party software) and delivering them to multiple targets, optionally transforming the data before forwarding.
- Pipes are designed for point-to-point integration: each pipe receives events from a single source and sends them to a single target while supporting richer data transformation and enrichment.
- Pipes and event buses are often used together: a pipe can ingest data from a DynamoDB Stream and send it to an event bus, which then distributes it to multiple destinations based on configured rules.
- EventBridge also includes EventBridge Scheduler — a serverless scheduler for cron or rate-based tasks and one-time executions, with configurable time windows and retry limits.

Essentially, EventBridge solves a common microservices challenge: how can components become aware of events happening elsewhere without direct API calls? Rather than writing complex cross-service request logic, one service emits an event to the bus, and interested services subscribe via rules to receive only the events they need. This approach allows adding or removing components without disrupting the rest of the system, which is ideal for projects that require scalability and maintainability over time.

---

### References

- [What Is Amazon EventBridge? – AWS Documentation](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)
- [Amazon EventBridge Event Buses – AWS Documentation](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-event-bus.html)
- [Amazon EventBridge Pipes – AWS Documentation](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-pipes.html)