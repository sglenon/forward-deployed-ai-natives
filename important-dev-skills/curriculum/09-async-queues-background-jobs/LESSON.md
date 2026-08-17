# Lesson: accepted work, workers, and recovery

## Learning goals

You will model a slow report operation as a job lifecycle, distinguish “accepted” from “completed,” and make repeated delivery safe. The notebook uses a deterministic in-memory queue so you can inspect every state transition without waiting or contacting a service.

## Why asynchronous work matters

Synchronous code makes a caller wait until the operation finishes. **Asynchronous** design lets a caller submit work and return while a worker finishes later. `async def` and `await` are Python syntax for cooperative waiting, but the deeper design is the lifecycle and recovery contract—not merely adding the keyword `async`.

If a report takes 60 seconds, a request should return a job ID and an **accepted** status. Accepted means the system recorded an intention to work; it does not mean the report exists. The client polls a status endpoint or receives a later notification.

## Vocabulary

- **Producer:** creates a job and places it where work can be found.
- **Queue:** an ordered or prioritized holding area for jobs.
- **Consumer/worker:** takes a job and performs its operation.
- **Job state:** durable label such as submitted, running, succeeded, failed, cancelled.
- **Durable:** survives a process crash because it is stored in a persistent system; an in-memory flag is not durable.
- **Acknowledgement (ack):** a signal that a delivery is finished and need not be redelivered.
- **At-least-once delivery:** a job may be delivered one or more times; loss is avoided at the cost of duplicates.
- **Idempotent effect:** repeating the same operation has the same business result as doing it once.
- **Outbox:** durable records of messages waiting to be published, reconciled after a crash.
- **Retry:** another attempt after a classified temporary failure.
- **Dead letter:** a visible terminal holding state for poison or exhausted jobs.
- **Backpressure:** slowing or rejecting producers when work exceeds safe capacity.

## The state-machine mental model

Think of a job as a small state machine:

```text
submitted -> queued -> running -> succeeded
                    |          -> retry_wait -> queued
                    |          -> failed/dead_letter
                    -> cancelled (only before work starts, by policy)
```

The allowed transitions are part of the contract. A client should not see `succeeded` before the result is stored. A worker should not acknowledge before a durable success or terminal failure is recorded.

## The crash windows

There are two important writes at submission: save job state and publish to the queue. If the process crashes after saving but before publishing, the job is accepted but invisible. An **outbox reconciliation** pass finds durable submitted jobs without a queue record and republishes them. If your real system has a transaction that atomically updates state and queue, use that instead; never hide this window.

At the worker, the effect can happen before acknowledgement. A crash in that window causes redelivery. At-least-once delivery therefore requires an idempotency key: the stable job ID is recorded with the report effect, and a duplicate sees the existing effect rather than creating another one. This proves the business effect is once for that key; it does not prove the worker ran once.

## Retry and poison work

A timeout or temporary dependency error may be retryable. Invalid input, a missing owner, or a deterministic schema error is usually permanent. Give retries a maximum attempt count and a next-attempt time. A message that keeps failing is a **poison message**; move it to dead letter so it cannot consume workers forever. Replay must be an explicit operator action that preserves identity and authorization.

## Cancellation and backpressure

Cancellation needs a race policy. If a queued job is cancelled before a worker claims it, skip it. If work is already running, cancellation may be cooperative and the effect may still finish; report that honestly. Never silently turn accepted work into cancellation because an HTTP request timed out.

If the queue is full, **backpressure** can reject new submissions with a bounded “try later,” or throttle producers. Do not accept a job and then drop it silently. Minimal payloads are safer: put a job ID and references in the queue, not secrets or huge documents.

## Worked example

```python
def submit(store, queue, owner, payload):
    job_id = store.create(owner, payload)
    queue.append(job_id)
    return {"status": 202, "job_id": job_id}

def worker_once(store, queue, effects):
    job_id = queue.pop(0)
    job = store.claim(job_id)
    if job is None:
        return "duplicate-or-cancelled"
    if job_id in effects:       # idempotency guard
        store.succeed(job_id, effects[job_id])
        return "already-done"
    result = make_report(job["payload"])
    effects[job_id] = result
    store.succeed(job_id, result)
    return "done"
```

The notebook adds controlled crashes between each line. Notice that `202` means accepted, not successful. A real durable store would need transactions or an outbox; the simulation makes the boundary explicit without pretending a list is durable.

## `async` and `await` in plain language

An `async def` function returns a coroutine, a description of work that can be scheduled. `await` pauses that coroutine while another task runs. This can improve use of one thread for waiting on I/O, but it does not make CPU-heavy work faster or make a queue durable. A background worker process, state store, acknowledgement rule, and recovery policy are separate design decisions.

## AI-generated queue code review

Check whether the generated code acknowledges early, catches every exception and loops forever, uses a random job ID on every retry, stores only an in-memory state, or claims exactly once. Ask it for a state diagram and failure matrix, then verify each queue API locally. Reject an abstraction unless a current test or replacement requires it.

## Syntax used in the notebook

`@dataclass` gives a small class predictable fields. `field(default_factory=dict)` creates a fresh dictionary for each store. `queue.pop(0)` consumes the next job; `queue.insert(0, job_id)` puts a redelivery first. A dictionary's `.get()` safely looks up an unknown job. The simulation uses ordinary calls instead of real scheduling so each transition is inspectable.

## Common mistakes

1. Returning completed when only durable submission happened.
2. Acknowledging before storing a result or terminal failure.
3. Reusing a new idempotency key for every retry.
4. Retrying invalid input forever instead of dead-lettering it.
5. Treating an in-memory state flag as durable recovery evidence.

## Knowledge checks — pause before answers

1. Why is a request timeout not proof that accepted work failed?
2. What crash window does an outbox reconcile?
3. Why can at-least-once delivery create duplicate effects?
4. What distinguishes a retryable error from a poison message?
5. Can a running job always be cancelled safely?

### Answers

1. The server may have recorded and continued the job after the client stopped waiting. Status must be queried separately.
2. It finds work saved durably but not published before a crash, then publishes it safely.
3. A worker may perform the effect and crash before ack, so the queue redelivers. An idempotency record prevents a second business effect.
4. A retryable error may succeed later; a poison message fails deterministically or has exhausted bounded attempts and needs visible operator handling.
5. No. If the effect is already running, cancellation may race and must be cooperative or report that completion can still occur.

## Notebook preparation

Open [lab.ipynb](lab.ipynb) with a fresh kernel. The fake clock advances by explicit calls, so there is no sleeping. Write down predictions before each run, attempt the guided state transition TODO, and keep the evidence handoff table.

## Summary and next connection

Asynchronous design is a contract about states, visibility, recovery, and honest client semantics. Persist intention, reconcile enqueue gaps, acknowledge after durable outcome, make effects idempotent, and bound retries. In Module 10 you will add correlated telemetry so an operator can see these transitions and diagnose where a job failed.
