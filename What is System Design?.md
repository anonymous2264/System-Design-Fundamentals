## INTRODUCTION

System Design... seems like a jargon... huh?

Welcome to my System Design notes repository.

I'm currently learning System Design and using this space to document everything I learn along the way. Instead of keeping notes scattered across notebooks and documents, I'm organizing them here so I can revise concepts quickly, track my progress, and share my learning journey with others.

System Design at its core focuses on how a system is structured to meet specific requirements at an expected SCALE.

I have intentionally kept a word in BOLD. Can you find it? Sure you can.

That's the word SCALE — perhaps the most important factor behind any successful system design.

Good system design defines how a system works, how data flows, which components handle specific tasks, and the trade-offs made to meet requirements. As applications grow in users, traffic, and data, simple architectures evolve by adding components such as load balancers, caches, queues, replicas, and monitoring systems to ensure scalability, reliability, and performance.

🎯 The aim is the SIMPLEST architecture that satisfies the requirements.

## CORE IDEA

System design is about making trade-offs under constraints.If users need low latency ,one may add caching or serve data from a closer location.If Availability is the main concern ... redundancy can be added.If write operation is saturating a database .. data can be partitioned.There is no perfect Design. Your design is as perfect as the number of problems you can handle.This is where the concept of trade-offs come into picture.

NEVER START FROM TECHNOLOGIES... ALWAYS START FROM THE PROBLEM

## FACTORS AFFECTING SYSTEM DESIGN
```
1.Requirements: What should a system do and importantly what it should not.
2.Scale: How many users,requests,writes,reads and amount of data it should handle?
3.Data: What type of data is stored,where it is stored and how it can be accessed? Formatting is essential.
4.Performance: What latency(Delay) and Throughput it must handle?
5.Consistency: Which operation can not afford incorrectness and which can partially tolerate it
6.Cost: Is the design feasible within a budget.
7.Communication: How do clients and servers communicate with each other.
```
NOTE: Even for the same service and functionality the design can be entirely different.Eg:- A chat app for a small team has different requirements than apps like Whatsapp and Twitter.

## BLOCKS
These are the modules which together build the system and acts as a template. We might not use all of them for surely most of them. Each of them solve a specific problem.
<img width="800" height="550" alt="image" src="https://github.com/user-attachments/assets/46c794bc-56bd-44c0-bd11-7edccff5bba2" />

• **Client** – Web app, mobile app, browser, or service that sends requests.

• **API Layer** – Exposes endpoints and handles communication between clients and backend services.

• **Load Balancer** – Distributes traffic across servers for scalability and high availability.

• **Application Servers** – Execute business logic and coordinate system operations.

• **Cache** – Stores frequently accessed data to reduce latency and database load.

• **Database/Storage** – Persists and manages durable application data.

• **Message Queue/Event Log** – Enables asynchronous processing and decouples services.

• **External Services** – Third-party integrations such as payments, email/SMS, authentication, and analytics.

• **Observability Stack** – Provides logging, monitoring, tracing, alerting, and dashboards for system health.

System design is less about listing these components and more about explaining how requests and data flow through them. The choices we make is real system design.

## APPROACHING A SYSTEM DESIGN PROBLEM

START SIMPLE----->> ADD COMPLEXITY ONLY WHEN NEEDED (Most important rule in all of system design).
<img width="866" height="181" alt="image" src="https://github.com/user-attachments/assets/0618374a-8603-4eb3-8161-163d48abb4b6" />

```
## Step 1: Tick the Requirements(Ask the questions)
- What are the core features?
- What users are you targettig?
- What we should not include?
- Scale
- Which operations must be correct and which needs low latency?
- What is the Availability Criteria?

For example, "users can view a timeline" is not enough. A timeline with 10,000 daily users can be generated differently from a timeline with 500 million daily users and a 200 ms latency target.
## Step 2: Estimate the Scale

Before designing a system, estimate its expected scale to understand potential bottlenecks and architectural requirements.

Consider:

* Read requests per second (RPS)
* Write requests per second (WPS)
* Storage growth over time
* Bandwidth requirements
* Peak traffic patterns
* Hot keys and uneven data distribution

The goal is not perfect calculations but identifying design pressures. A system handling 100 writes/second will have very different challenges from one handling 1 million writes/second.

---

## Step 3: Start with a Simple Architecture

Begin with the smallest architecture that satisfies the requirements:

1. Client
2. API Layer
3. Application Service
4. Database

Add complexity only when necessary:

* **Cache** → Reduce latency and database load
* **Queue** → Handle asynchronous tasks and traffic spikes
* **Replicas** → Improve read scalability and availability
* **Partitioning (Sharding)** → Increase storage and write capacity
* **Regional Deployment** → Reduce latency and improve resilience

Real-world systems evolve gradually as new constraints emerge.

---

## Step 4: Identify Bottlenecks and Failure Modes

Once the baseline architecture is defined, analyze possible weaknesses.

Questions to consider:

* What if the database fails?
* What if traffic suddenly increases 10x?
* What if the cache becomes unavailable?
* What if queue consumers fall behind?
* What if a third-party service becomes slow or unavailable?
* Which data can tolerate staleness?
* Which operations require strong consistency?

A good design anticipates failures and explains how the system behaves under them.

---

## Step 5: Explain Trade-offs

Every design decision introduces benefits and costs.

| Decision         | Benefit                               | Trade-off                        |
| ---------------- | ------------------------------------- | -------------------------------- |
| Caching          | Lower latency                         | Cache invalidation complexity    |
| Replication      | Higher availability & read throughput | Consistency lag                  |
| Sharding         | Better write scalability              | Increased operational complexity |
| Async Processing | Handles traffic spikes efficiently    | Delayed results                  |

Strong system design is not about finding a perfect solution; it is about choosing the most appropriate trade-offs for the given requirements.
```
## Conclusion

System Design is the art of turning requirements into scalable, reliable, and efficient architectures. Every design choice solves a problem while introducing trade-offs, making design judgment one of the most important skills for engineers. The key is to understand why a component exists, what problem it solves, and whether its trade-offs are worth it.
