# Module 13: Scalability and production system design

## Outcome

Reason from measurements to the next likely bottleneck as a service grows from tens to thousands and then hundreds of thousands of users.

## Lab progression

1. Establish a workload model: request mix, data size, latency target, and concurrency.
2. Profile the baseline before proposing architecture.
3. Identify state that prevents horizontal scaling.
4. Test database connection, query, CPU, memory, and external-service limits.
5. Add one evidence-backed improvement such as indexing, caching, batching, or rate limiting.
6. Define cache ownership, invalidation, and failure behavior.
7. Draw failure domains and remove one avoidable shared failure.
8. Repeat the load test and name the next bottleneck.

## Required evidence

- Assumptions and a simple capacity model.
- Reproducible load-test configuration and baseline results.
- Profiles or resource measurements supporting the chosen change.
- A before-and-after comparison including latency, throughput, errors, and resource cost.

## Pass conditions

- The learner distinguishes latency from throughput.
- Scaling recommendations follow observed constraints.
- Rate limits and overload behavior protect the system predictably.
- Cache behavior cannot silently serve prohibited or cross-tenant data.
- The design avoids premature service decomposition without a demonstrated boundary.
