# Module 6: Database performance and transactions

## Start here

Performance is a measured property, not a guess. A **query plan** describes how a database intends to find rows. A **transaction** groups changes so they commit together or roll back together. In a bounded in-memory SQLite lab you will expose an N+1 query pattern, inspect `EXPLAIN QUERY PLAN`, apply one isolated intervention, and protect a state transition with optimistic concurrency.

You should know SQL from Module 5. Timing examples are intentionally stable: correctness and query counts matter more than flaky millisecond thresholds.

## Vocabulary preview

- **Latency:** elapsed time for one operation.
- **Query plan:** the database's intended strategy for finding and joining rows.
- **Index:** an auxiliary structure that can speed a matching lookup.
- **N+1 query:** one parent query followed by one child query per parent.
- **Transaction:** a group of database changes committed or rolled back together.
- **Lost update:** a later write silently overwriting a concurrent earlier change.
- **Optimistic concurrency:** detecting a stale version instead of silently overwriting it.

The full [lesson](LESSON.md) explains these terms with one measured local experiment.

## What you will know and do

- measure query count, bounded timing, rows, and plan evidence;
- explain indexes, composite indexes, N+1, and why an index has write/storage cost;
- explain ACID, lost updates, optimistic version checks, locking, deadlocks, bounded retries, and connection pooling conceptually;
- isolate one performance intervention per experiment and release failed transactions;
- review AI advice against observed plans rather than column-name intuition.

## Study order and time

Read [LESSON.md](LESSON.md), write separate performance/concurrency hypotheses, then run [lab.ipynb](lab.ipynb). Plan 90–150 minutes with a bounded synthetic fixture.

## Completion checklist

- [ ] I captured baseline query count and plan evidence.
- [ ] I identified N+1 and made one attributable change.
- [ ] I verified result/order correctness after the change.
- [ ] I demonstrated one winner and one explicit conflict for concurrent updates.
- [ ] I tested rollback and bounded retry logic without real sleeping.
- [ ] I documented pool limits and what this local experiment cannot prove.

## Evidence and pass conditions

Keep comparable before/after counts, plans, fixture size, one-intervention rationale, concurrency results, transaction boundary, rollback/retry evidence, pool assumptions, and AI review. Pass means performance claims have measured support; no update is silently lost; retries are bounded/replay-safe; and claims do not exceed the local fixture.

## Next module

Continue to [Module 7: Error handling and resilience](../07-error-handling-resilience/README.md), where failures become explicit client and operator contracts.
