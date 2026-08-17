# Lesson: measure queries and protect changes

## Learning goals

You will count queries, read a SQLite query plan, make one isolated performance change, and use a version check to prevent a lost update.

## Performance is evidence

**Latency** is elapsed time. **Throughput** is work completed per unit time. A benchmark is meaningful only with a bounded fixture, query count, input distribution, and repeatable method. Milliseconds in an in-memory database are noisy; this lesson emphasizes query count and plan shape.

An **index** is an auxiliary ordered structure that helps find rows without scanning every row. It speeds some reads but consumes space and makes writes more expensive. A composite index covers multiple columns in an order that should match a real filter/order pattern. Do not add indexes because a column “looks important.”

## N+1 and plans

The **N+1 query problem** happens when code runs one query to fetch N parents, then one child query per parent. Query count grows with data size. A join or batch query can fetch the same information in a small fixed number of queries. `EXPLAIN QUERY PLAN` shows whether SQLite scans a table or uses an index; it is evidence about access strategy, not a promise of production latency.

The lab's query counter is a tiny wrapper around `execute`. First capture baseline count/results, then make exactly one change and compare the same fixture. Preserve ordering and output. If you add an index, explain its write/storage cost separately.

## ACID and transaction boundaries

A **transaction** groups database operations. ACID names four goals: atomic (all or none), consistent (rules remain true), isolated (concurrent work is controlled), and durable (committed work survives the database's guarantees). `BEGIN`, `COMMIT`, and `ROLLBACK` mark the boundary. Keep it short and always roll back on error.

A **lost update** occurs when two readers see version 1, both compute a change, and the later write silently overwrites the earlier one. Optimistic concurrency detects this with a version column:

```sql
UPDATE tasks SET state=?, version=version+1
WHERE id=? AND version=?
```

If affected rows equal zero, someone won or the row disappeared; return an explicit conflict. This is safer than assuming the read is still current.

## Locks, retries, and pooling

A **lock** temporarily prevents conflicting access. A **deadlock** is a cycle where each transaction waits for another; consistent lock order, short transactions, and bounded retries help. Retry only a classified, replay-safe operation. A **connection pool** reuses a bounded number of database connections; callers must return them even on failure. The lab models pool exhaustion conceptually and does not claim capacity from one process.

## Common mistakes

1. Calling a benchmark “faster” after changing fixture size or result ordering.
2. Adding three indexes at once, so no effect is attributable.
3. Treating a plan that uses an index as proof every workload improves.
4. Retrying a transaction that already performed a non-idempotent external side effect.
5. Catching an exception without rollback/releasing the connection.
6. Reading a version then updating without including the version in the `WHERE` clause.

## Reviewing AI-generated performance code

Ask for the observed query, plan, fixture, and access pattern before accepting an index. Inspect parameterization, result equivalence, stable ordering, transaction scope, isolation assumptions, affected-row conflict handling, retry count, and resource release. Reject timing assertions that fail randomly, unbounded load loops, and pool-size changes used to hide N+1.

## Knowledge checks — pause before answers

1. How does N+1 query count change as parent count grows?
2. What does an index cost besides helping reads?
3. Why does a version in the `WHERE` clause detect a lost update?
4. What must happen to a transaction and connection after an exception?
5. Why should performance interventions be isolated?

### Answers

1. It grows roughly one child query per parent, so N parents cause about N+1 queries.
2. It consumes storage and adds work to inserts, updates, and deletes.
3. A stale reader's version no longer matches, so its update affects zero rows instead of overwriting the winner.
4. Roll back unfinished work and return/release the connection in cleanup.
5. Otherwise you cannot tell which change caused an improvement or regression.

## Notebook preparation

Use a bounded in-memory SQLite fixture and write two hypotheses: one about query count/plan, one about conflict handling. No real sleeps or unbounded concurrency are needed. Record counts and representative plans, then restart before final execution.

## Summary and next connection

Measure the same work, inspect a plan, and make one attributable change. Transactions provide atomic boundaries; optimistic version checks turn silent overwrites into explicit conflicts. Retries need classification and replay safety, and pools need cleanup. Next, you will design the client-facing behavior when any dependency fails.

## A slower walkthrough: read a query plan

Start with the question “find children for parent 2.” Without an index, SQLite may scan every child row and test `parent_id`. With an index on `children(parent_id)`, it can search the index for matching keys and then visit the matching rows. The important evidence is not that the word “index” sounds good; it is that the plan changed for a real filter and the returned rows stayed identical. A plan is an explanation of one access strategy, not a universal speed guarantee.

### Why N+1 is a shape problem

For one parent, a first query plus one child query may look harmless. For 100 parents it becomes 101 queries, often with repeated network/connection overhead. A join asks the database for the relationship in one statement. A batch query (`WHERE parent_id IN (...)`) is another option. Keep ordering explicit because a join can otherwise return rows in an order the caller did not promise. Measure query count on the same fixture before and after one intervention.

### A transaction story

Imagine two workers reading an item with `version = 1`. Worker A decides “done”; worker B decides “cancelled.” Without a guard, whichever writes last silently erases the other decision. With `WHERE id=? AND version=?`, A changes one row and increments the version to 2. B changes zero rows and can return a conflict or re-read. This is **optimistic concurrency**: assume conflicts are uncommon, detect them, and let the caller decide what to do.

ACID is a memory aid, not a magic switch. Atomicity says a transaction's own changes commit together. Isolation describes what concurrent transactions can observe and depends on the database and level. Durability depends on the database's storage guarantees. A short transaction with a clear rollback path is easier to reason about than a transaction that waits on network calls. If a retry is added, ask whether every operation inside it is replay-safe.

## Measurement notes for beginners

Never compare two timings after changing fixture size, cache state, query shape, or output ordering. In a tiny in-memory database, timing noise can exceed the change. Query count, plan output, result equivalence, and bounded repeated samples are better learning evidence. A connection pool is also not a performance button: a larger pool can increase contention and hide a query problem. Always return a connection after both success and failure.

## A worked experiment you can explain to a mentor

1. State the access pattern: “list each parent with its children, ordered by parent then child ID.”
2. Freeze the fixture: three parents, four children, and one local connection.
3. Count baseline queries and save the returned rows.
4. Write the hypothesis that a join will keep the rows while reducing query count.
5. Change only the read shape, not the schema, fixture, or ordering.
6. Count again, compare rows, and inspect the query plan.

If the result changes, the experiment failed even if the count improved. If the result stays the same, the count and plan support a local improvement. They do not prove an improvement for a different database, network, cache, data distribution, or production workload. This style of evidence is more trustworthy than an AI answer that names an index without looking at the query.

## Transaction vocabulary in plain language

The connection is the channel to the database. A transaction is the period in which a set of statements is treated as one unit. A commit makes the unit visible according to the database's rules; a rollback abandons its unfinished changes. A version is a number that changes with each successful update. A conflict is not the same as a database crash: it tells the caller that its snapshot is stale and invites a deliberate reread or merge.
