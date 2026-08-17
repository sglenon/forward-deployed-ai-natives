# Lesson: measure a bottleneck before designing for scale

## Learning goals

You will define a workload, separate key capacity terms, use deterministic measurements to choose one intervention, and name the next bottleneck and the limits of your evidence.

## Vocabulary

- **Workload model:** assumptions about requests, users, records, payloads, and read/write mix.
- **Latency:** time for one request; p95 means 95% of observations are at or below that value.
- **Throughput:** completed work per unit of time.
- **Concurrency:** work in progress at one moment.
- **Capacity:** the maximum sustainable workload under a quality target.
- **Bottleneck:** the constrained resource that limits the whole path.
- **Vertical scaling:** giving one instance more resources.
- **Horizontal scaling:** adding instances.
- **Stateless:** any instance can serve a request because session state is not trapped in one process.
- **Connection pool:** a bounded set of reusable database/dependency connections.
- **Pagination:** returning a bounded slice rather than an unbounded list.
- **Cache:** stored result reused for a period; invalidation decides when it is stale.
- **Failure domain:** a component or zone that can fail together.

## Why architecture diagrams are not measurements

An architecture can look scalable while one unbounded query or shared session limits it. Start with a target, such as p95 under 100 ms for a stated synthetic workload. Record assumptions for 10, 1,000, and 100,000 users; label them assumptions, not facts. A local simulation can compare two designs under its model, but cannot promise production performance.

## Little’s law as intuition

For a stable system, average concurrency is approximately throughput × average latency. If five requests per second each take two seconds, roughly ten requests are in progress. This relationship helps you see why increasing concurrency does not automatically increase throughput: the bottleneck may saturate.

## Find the constrained resource

Candidate bottlenecks include CPU, memory, a slow query, connection pool, dependency, serialization, lock, or network. Measure more than one signal. If list latency grows with record count while CPU stays low and the query lacks an index, the query is a stronger hypothesis than “add servers.” If a dependency delay dominates spans, a timeout or fallback may be the bounded change.

## One intervention per experiment

Possible bounded changes: enforce page size, add an index for a measured predicate, cache a safe key with TTL and invalidation, batch calls, rate-limit a client, or add a dependency timeout. State the expected metric change before editing. Change one thing, rerun the identical workload, and compare fake p50/p95/p99-style values, throughput, errors, and resource counters. Combining pagination, cache, and a new database makes causality unclear.

## Statelessness, caches, and failure behavior

Horizontal scaling works best when instances are stateless. A process-local session or cache can cause users to see different behavior when requests move between instances. A cache key must include tenant/owner scope. Define stale data and invalidation behavior, and decide what happens when the cache is unavailable: bypass, fail closed, or serve a bounded stale value.

Rate limits and backpressure keep overload honest. Pagination protects response size. Timeouts protect callers from indefinite waits but may leave work running; pair them with cancellation or asynchronous status when appropriate. Every limit needs a documented response.

## Failure domains and service boundaries

A failure domain is a part that can fail together. Splitting a service creates network and deployment failure domains; it is not automatically an improvement. Mark database, dependency, cache, queue, and instances on a small diagram. Ask which boundary isolates failures and which merely moves the bottleneck.

## Build a capacity model with arithmetic

A capacity model is a transparent estimate, not a prophecy. Start with named assumptions. Suppose a fictional team has 1,000 registered users, 10% active in an hour, and each active user makes 6 requests per minute. The average request rate is:

```text
1,000 users × 0.10 active × 6 requests/minute ÷ 60 = 10 requests/second
```

If 80% are reads and 20% are writes, that is 8 read requests/second and 2 writes/second. A short burst can be higher than the hour average, so write down a burst multiplier rather than quietly assuming the average is safe. At 10, 1,000, and 100,000 users, apply the same assumptions and show the arithmetic. If an assumption is unknown, label it unknown and run a sensitivity check (for example, active users at 10% versus 30%).

Capacity also needs a quality target. “The service handles 10,000 users” is incomplete; “under this workload, p95 list latency stays below 100 ms, errors stay below 1%, and the queue remains below 100 jobs” is testable. The sustainable limit is the highest measured workload that stays within those targets for the chosen window. A single fast request is not a capacity result.

## Read latency, throughput, and concurrency together

Latency is the duration experienced by one request. Throughput is completed requests per unit of time. Concurrency is the number of requests currently in progress. They interact but are not synonyms. If a worker completes 20 requests per second and each takes 0.5 seconds on average, approximately `20 × 0.5 = 10` requests are in progress. If a database can serve only 10 concurrent queries, increasing clients beyond that point creates a waiting line; it does not create more database capacity.

Percentiles describe that line better than an average. If nine requests take 10 ms and one takes 200 ms, the average is 29 ms, but one in ten users sees 200 ms. A p95 or p99 target makes tail behavior visible. The notebook uses deterministic samples rather than a real clock; in a real service, keep the workload, sample count, and percentile method the same before and after an experiment.

## Turn a bottleneck guess into evidence

Write a falsifiable hypothesis: “When records grow from 1,000 to 10,000, the unbounded list query drives p95 because query time rises while CPU and dependency time stay roughly constant.” Then choose measurements that could disprove it:

| Observation | Supports query bottleneck | Weakens query hypothesis |
| --- | --- | --- |
| query duration | rises with record count | stays flat |
| CPU | remains low | reaches saturation |
| dependency span | remains small | dominates total latency |
| connection use | below pool limit | pool is exhausted |

Evidence should include a fixture identifier, request mix, record count, page size, and safety limit. Mark each conclusion as evidence, assumption, or unknown. If the measurements disagree, keep the hypothesis open; do not choose an architecture because an AI diagram looks convincing.

## Cache correctness and failure behavior

A cache is a copy with a freshness policy. Define its key, time-to-live (TTL), and invalidation event before using it. A notes cache key must include owner or tenant identity, resource ID, and any representation-affecting options. When a note changes, either delete the old key, update it transactionally, or accept a documented stale window. “Add a cache” without invalidation can serve old authorization or content indefinitely.

Decide what happens when the cache is unavailable. A read-through cache may bypass to the database (higher latency), fail closed for sensitive data, or serve bounded stale data with an explicit marker. A write path must not report success merely because a cache write succeeded if the database write failed. Test hit, miss, expired entry, invalidation, tenant separation, and cache outage as separate behaviors.

## Why one intervention makes a defensible experiment

A bounded experiment changes one cause while holding the workload and fixture constant. If you add pagination and an index together and latency improves, you cannot tell which change mattered or whether one hides a regression. Record the predicted metric change before editing, run the baseline, make one change, rerun the same cases, and state what did not improve. A rollback condition—such as “revert if p95 improves but error rate rises above 1%”—turns a demo into a decision record.

## AI design review

Ask an AI tool for measurements and adversarial cases before asking for architecture. Verify APIs, cache semantics, index predicates, connection limits, and configuration versions. Reject unbounded retries, global caches without tenant keys, speculative microservices, and any generated claim not supported by your run. Review the entire diff, including tests and configuration.

## Syntax used in the notebook

The simulation uses dictionaries for measurements and a function with optional arguments (`page_limit=None`) for two candidate designs. `min(records, page_limit)` bounds work. Arithmetic creates deterministic latency and throughput; `assert` checks the contract. There is no `time`, thread, subprocess, or network call.

## Common mistakes

1. Calling latency, throughput, concurrency, and capacity interchangeable words.
2. Increasing traffic before defining a safe workload and restoring fixtures.
3. Changing pagination, caching, and schema together and losing causal evidence.
4. Building a cache key without owner/tenant identity or an invalidation policy.
5. Treating a tiny local simulation as a production capacity guarantee.

## Knowledge checks — pause before answers

1. How are latency and throughput different?
2. Why can adding concurrency make a saturated database worse?
3. What makes a cache key unsafe in a multi-tenant service?
4. Why should experiments change one intervention at a time?
5. Name one capacity claim a local simulation cannot defend.

### Answers

1. Latency is duration for one operation; throughput is completed operations per time.
2. More in-flight requests compete for the same constrained connections/CPU and can increase queueing and latency.
3. If it omits tenant/owner identity, one tenant may receive another tenant's cached result.
4. Otherwise an improved metric cannot be attributed to one cause.
5. A local fake run cannot prove a production cloud region's maximum users, real network behavior, or failure recovery.

## Notebook preparation

Open [lab.ipynb](lab.ipynb) with a fresh kernel. The fake measurements are lists and formulas, not real load. Predict the likely bottleneck, attempt the one-change TODO, and preserve the decision record and evidence handoff.

## Summary and next connection

Scalability is a measured claim under explicit assumptions. Define workload and quality targets, find the constraint, make one bounded change, and test overload and failure semantics. Module 14 will use hypothesis-driven debugging and AI diff review to challenge the assumptions behind your measurement.
