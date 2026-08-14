# Module 6: Database performance and transactions

## Outcome

Diagnose a slow endpoint from its query plan and protect a concurrent state change with an appropriate transaction strategy.

## Lab progression

1. Measure a deliberately slow list or detail endpoint with realistic data volume.
2. Capture generated SQL and identify N+1 behavior.
3. Read `EXPLAIN` or the database’s equivalent plan.
4. Add or change queries and indexes based on observed access patterns.
5. Simulate two users modifying the same record concurrently.
6. Choose locking, optimistic concurrency, or a database constraint for the conflict.
7. Force a deadlock or serialization failure and handle it safely.
8. Check connection-pool behavior under bounded load.

## Required evidence

- Before-and-after latency and query counts.
- Query plans before and after the selected index or query change.
- A concurrency test that fails on the baseline and passes on the final design.
- A transaction-boundary diagram and retry decision.

## Pass conditions

- Performance claims use measured data rather than intuition.
- The chosen index supports a real query and its write cost is acknowledged.
- The state transition cannot silently lose an update.
- Transaction retries are bounded and replay-safe.
- Pool limits and failure behavior are explicit.
