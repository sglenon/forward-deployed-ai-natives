# Module 9: Async processing, queues, and background jobs

## Outcome

Move a slow request into a queue-backed worker flow that survives duplicate delivery, worker failure, and permanent job errors.

## Lab progression

1. Measure a request that blocks for a long-running operation.
2. Define the submitted, running, succeeded, and failed job states.
3. Return an accepted response with a stable job identifier.
4. Implement a producer, worker, and result query.
5. Crash the worker after applying the business action but before acknowledging the job.
6. Make job handling idempotent under at-least-once delivery.
7. Add bounded retry and a dead-letter path for permanent or exhausted failures.
8. Add safe replay and cancellation behavior.

## Required evidence

- A sequence diagram for request, queue, worker, store, and client.
- Tests for duplicate delivery, crash recovery, poison messages, and retry exhaustion.
- A demonstration that API timeout no longer cancels accepted work accidentally.
- An operator procedure for inspecting and replaying failed jobs.

## Pass conditions

- The API communicates asynchronous acceptance rather than false completion.
- Duplicate jobs do not duplicate the business effect.
- Failed work remains visible and owned.
- Retry does not loop without limit.
- Job status and cancellation semantics are explicit.
