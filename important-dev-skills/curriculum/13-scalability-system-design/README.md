# Module 13: Scalability and production system design

## Start here

Scalability means handling more work while keeping an explicit quality target. You will run a deterministic capacity simulation, identify one bottleneck from fake measurements, and make one bounded intervention. There is no real load generation or timing flakiness.

Assume Modules 1–12: SQL, queues, telemetry, security, and deployment. [LESSON.md](LESSON.md) defines every new term before the notebook uses it.

## Vocabulary preview

- **p95 latency:** a duration at or below which 95% of observations fall.
- **Throughput:** completed work per unit of time.
- **Concurrency:** work in progress at one moment.
- **Capacity:** sustainable workload under a stated quality target.
- **Bottleneck:** the constrained resource limiting the whole path.
- **Statelessness:** any instance can serve because session state is not trapped locally.
- **Cache invalidation:** deciding when a stored copy is no longer safe to use.
- **Failure domain:** components that can fail together.

## What you will know and do

- write a workload and capacity model with assumptions;
- distinguish latency, throughput, concurrency, and capacity;
- find a bottleneck using measurements rather than diagrams;
- evaluate pagination, indexes, caches, batching, and rate limits;
- run one intervention per experiment and explain failure behavior;
- state what a tiny local simulation cannot prove.

## Study order and time

Read [LESSON.md](LESSON.md), answer checks, then run [lab.ipynb](lab.ipynb). Preserve before/after fake measurements and the decision record.

## Completion checklist

- [ ] I wrote three predictions about capacity or bottlenecks.
- [ ] I labeled assumptions, evidence, and unknowns.
- [ ] I measured a baseline before choosing a change.
- [ ] I changed one bounded component and reran the same workload.
- [ ] I tested invalid, empty, overloaded, and dependency-failure behavior.
- [ ] I named the next bottleneck and an unsafe capacity claim.

## Evidence and pass conditions

Keep workload assumptions for 10/1,000/100,000 users, deterministic before/after p50/p95/p99-style results, failure checks, one-component diff, AI review, and a failure-domain sketch. Include cache key/invalidation behavior and rollback conditions. You pass when the change follows measured evidence, preserves tenant isolation, has explicit limits, and is reproducible without claiming production scale.

## Next module

Continue to [Module 14: Debugging and AI code review](../14-debugging-ai-code-review/README.md), which applies hypothesis-driven diagnosis to the system you have now measured.

Previous: [Module 12: Docker, environments, and CI/CD](../12-docker-environments-cicd/README.md).
