# Stage 6. Architecture and design (ongoing)

Architecture isn't diagrams or a buzzword, it's the answer to the question of what the system will look like in two years if the team triples and the business model shifts. At the senior level companies value engineers who pick simple solutions and understand when and why to add complexity.

## Principles and foundation

* SOLID without fanaticism. The real cost of every principle: extra abstractions slow down change, missing abstractions break isolation. Be able to explain when violating SOLID is justified.
* Cohesion and coupling matter more than literal principle compliance. High cohesion inside a module and low coupling between modules usually solves 80% of design problems.
* YAGNI and KISS as a counterweight to over-engineering.
* Conway's law: the system's architecture mirrors the team's structure. It works both ways.

## Domain-Driven Design

* Strategic DDD: bounded contexts, ubiquitous language, context maps. More important than tactical patterns.
* Tactical DDD: aggregates, value objects, entities, repositories, domain events. Apply where business logic is complex, not on CRUD.
* Event Storming as a way to build a shared model with product managers and analysts.
* Books: "Domain-Driven Design" by Eric Evans as the foundation, "Implementing DDD" by Vernon as a practical guide, "Learning Domain-Driven Design" by Vlad Khononov as a modern introduction.

## Architectural styles

* Clean Architecture, Hexagonal, Onion. Be able to explain what problem each solves and what their shared core is (isolating the domain from infrastructure).
* Vertical Slice Architecture as an alternative to layered approaches for teams that care most about feature delivery speed.
* The modular monolith is a sensible starting point almost always. Move to microservices once domain boundaries are clear and there's a platform team.
* Microservices: when they're justified (organizational constraints, different SLAs, independent scaling), when they aren't (small team, immature platform).

## Patterns and integrations

* CQRS with MediatR or without it, when reads and writes have different requirements.
* Event Sourcing where change history matters (finance, audit). Understand the complications: projections, event versioning, replays.
* Outbox pattern for reliable event publishing from inside a transaction.
* Saga for distributed processes: choreography vs orchestration.
* Idempotency keys for safely retrying payments and critical operations.
* Polly: Retry with exponential backoff, Circuit Breaker, Timeout, Bulkhead. Apply them deliberately; retry without jitter turns into a DDoS on your own service.

## Queues and brokers

* RabbitMQ for classical message-queue scenarios, Kafka for event streaming and large volumes.
* Azure Service Bus, AWS SQS, Google Pub/Sub in cloud stacks.
* MassTransit as a broker abstraction in the .NET world, with Saga and Outbox out of the box.
* Delivery guarantees: at-most-once, at-least-once, exactly-once (a myth in distributed systems, achieved through idempotency).

## Distributed systems

* The CAP theorem and its limitations, PACELC as a more precise model.
* Eventual consistency and trade-offs: read-your-writes, monotonic reads.
* Distributed transactions via 2PC are almost always a bad idea; Saga and Outbox are usually better.
* Timing: timeouts, deadlines, retry budgets, backpressure.

## Resources

* "Designing Data-Intensive Applications" by Martin Kleppmann — the backend book of the decade.
* "Building Microservices" by Sam Newman, second edition.
* "Software Architecture: The Hard Parts" by Neal Ford et al.
* "Fundamentals of Software Architecture" by Mark Richards and Neal Ford.
* Vladimir Khorikov's blog (enterprisecraftsmanship.com), especially posts on DDD and testing.
* The CodeOpinion YouTube channel (Derek Comartin) for breakdowns of DDD, CQRS, messaging.
* Martin Fowler's blog (martinfowler.com), a genre classic.

## Practice

1. Design a modular monolith for a medium-sized domain (delivery, booking, marketplace) with explicit contexts and inter-context contracts.
2. Implement the Outbox pattern in one of your services and walk through a DB-and-broker failure scenario.
3. Introduce CQRS in a section where it's justified and honestly describe what you gained and what you lost.
4. Write an ADR (Architecture Decision Record) for 3–4 key project decisions.

## Readiness signals for the next stage

* You can run Event Storming with a product team and walk out with a working domain map.
* You can explain the difference between choreography and orchestration in a Saga and give an example of when each fits.
* You've implemented Outbox with tests for retries and failures.
* You can defend choosing a modular monolith in front of a team that wants "like at Netflix."

## Back to navigation

[All stages](README.md) | [Main README](../README.md)
