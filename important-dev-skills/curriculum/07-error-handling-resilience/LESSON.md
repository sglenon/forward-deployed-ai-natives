# Lesson: fail honestly and recover deliberately

## Learning goals

You will classify failures, map them to safe responses, enforce bounded time and attempts, make a write replay-safe, and model truthful degradation with deterministic fakes.

## Failure is part of the contract

A **failure category** is a useful label for what went wrong. Validation/domain errors mean the request or business state is unacceptable. A transient dependency error may succeed later. A permanent error will not succeed by retrying the same input. A timeout means the deadline passed; cancellation means the caller or shutdown asked us to stop. An unexpected defect is a programming problem that should be visible to operators, not disguised as a client validation error.

Make a failure matrix before code: category, client status/code, internal evidence, retry decision, and recovery owner. **Propagation** means carrying an error to a boundary without losing its meaning. One application boundary can translate expected errors to a stable safe body; it should not catch every exception and claim success.

## Safe responses and correlation

A client needs an actionable code, not a traceback. Return a stable body such as `{"error": {"code": "dependency_unavailable", "request_id": "r-1"}}`. A **correlation/request ID** connects client output to internal logs without exposing stack traces, SQL, secrets, or raw dependency bodies. Internal logs should record category, attempt count, and safe context. Unexpected defects generally become a generic `500` while preserving diagnostics internally.

## Deadlines and classified retries

A **deadline** is the latest time an operation may finish. A timeout must be enforced at the dependency boundary; “we will probably finish soon” is not a bound. A **retry** repeats an operation after a failure. Retry only transient failures and only when replay is safe. A **backoff** increases the delay between attempts; **jitter** adds small randomness so many clients do not retry together. In the notebook, a fake sleeper records requested delays instead of sleeping.

Use a small maximum attempt count and a total budget. Do not retry validation, permanent failure, cancellation, or an unknown side effect. An error after a dependency accepted a request is **ambiguous**: the client may retry, so the write needs an idempotency key or another deduplication method.

## Idempotency and truthful degradation

An **idempotency key** names one intended write. Store the key and result before returning, then replay the stored result for the same request fingerprint. If process failure occurs after the business effect but before recording completion, exactly-once behavior is not proven; document reconciliation or an outbox/queue design instead.

A **circuit breaker** stops sending requests after repeated failures, then allows a controlled trial after a cooldown. A fallback is safe only if it tells the truth. Returning a fake report for missing source data is not graceful degradation; queueing work with a visible `202` “accepted for later” can be truthful if the system really stores it. **Cancellation** should stop new work and avoid claiming success; shutdown needs a bounded drain policy.

## Common mistakes

1. `except Exception: return success` hides defects and corrupts trust.
2. Retrying every exception, including a non-idempotent write.
3. Having a timeout parameter that the dependency ignores.
4. Sleeping in tests and asserting wall-clock milliseconds.
5. Returning raw dependency messages or exception text to clients.
6. Calling a fallback “success” when work was dropped or only partially done.

## Reviewing AI-generated resilience code

Trace every exception class and state transition. Ask: what is the maximum attempts/time? Is the dependency call actually bounded? Is the retry safe after an ambiguous response? Where is the idempotency record? Does cancellation skip success? Does the breaker reset deterministically? Inspect logging for secrets and response bodies. Reject infinite loops, broad catches, real sleeps in tests, and “exactly once” claims without crash-window evidence.

## Knowledge checks — pause before answers

1. Why should a permanent dependency error not be retried?
2. What does a deadline guarantee that a retry count alone does not?
3. Why can a timeout after a write be ambiguous?
4. What makes a fallback truthful?
5. Which details belong in internal evidence but not a client body?

### Answers

1. Repeating the same request will not repair a permanent condition and may waste time or amplify load.
2. A deadline bounds total waiting time; a retry count does not bound how long each attempt can hang.
3. The dependency may have completed the write even though the response did not arrive, so retrying can duplicate it.
4. It reports exactly what happened and preserves recoverable work, such as an actually stored queued job, rather than inventing success.
5. Stack traces, SQL, dependency URLs/bodies, and secret-bearing context help operators but can leak internals or sensitive data to clients.

## Notebook preparation

Open [lab.ipynb](lab.ipynb) with a fresh kernel. The fake dependency returns scripted outcomes; the clock and sleeper are deterministic. Record a failure matrix, baseline side-effect count, final attempts, safe response, and correlation ID. No actual waiting or network is involved.

## Summary and next connection

Resilient code names failure categories, centralizes translation, bounds time and retries, and makes side effects replay-safe. It degrades only in ways that remain true and leaves unresolved recovery visible. Next, testing techniques will help you keep these contracts true as production code changes.

## A slower walkthrough: classify before acting

Consider a report request with a title and a source dependency. If the title is missing, retrying cannot fix it; return a validation error. If the source says “not found” permanently, retrying the same lookup wastes work. If the source returns a documented temporary-unavailable error, one or two bounded retries may help. If the call exceeds its deadline, stop waiting and tell the caller the result is uncertain. If Python raises an unexpected `KeyError`, do not relabel it as invalid input; return a safe generic error and preserve diagnostic evidence for an operator.

The category determines four choices: what the client sees, whether to retry, whether work may have happened, and who owns recovery. A failure matrix makes these choices visible before code. It also prevents an AI-generated `except Exception` from erasing the distinction between a caller mistake and a programming defect.

## Timing and the ambiguous write

Suppose the service writes a report and then waits for the response from a dependency. The dependency may finish the write just as the client's deadline expires. A retry now has two possible realities: the first write succeeded, or it did not. This is an ambiguous outcome. An idempotency key lets the service recognize the same intended operation and return the recorded result instead of creating another report. It does not remove the crash window between effect and recording; a responsible design documents reconciliation, an outbox, or a queue rather than promising exactly once.

### Backoff in a concrete example

With maximum attempts three, an implementation might record delays `[1, 2]` before the final attempt. The delays are evidence that waiting is bounded, not a reason to make a test sleep. Jitter adds a small random component in real systems to avoid synchronized retry storms; deterministic tests can inject a fake random source or test only the bounds. Never retry cancellation merely because it is an exception—shutdown is an instruction to stop work.

## Honest degradation and shutdown

A circuit breaker protects a failing dependency by moving from closed to open after repeated failures, then allowing a controlled half-open trial after a clock-based cooldown. A fallback is truthful only when the promised alternate state exists. Returning a fake report is dishonest; storing a real job and responding “accepted for later” can be truthful. During shutdown, stop accepting new work, cancel or drain existing work within a bound, release resources, and never return success for an operation that was abandoned.

## A worked failure table

| Situation | Client result | Retry? | Evidence |
| --- | --- | --- | --- |
| Missing title | stable 400 code | no | validation field |
| Temporary source outage | 503 after a small budget | yes, bounded | attempt count |
| Source says permanently absent | 502/404 by contract | no | dependency category |
| Deadline exceeded | timeout code | only if safe | elapsed budget |
| Duplicate key | original result | no new effect | stored fingerprint |
| Programmer defect | generic 500 | no automatic retry | request ID + internal trace |

Walk through this table before writing a `try` block. It prevents a catch-all from choosing the retry policy by accident. It also gives a mentor a way to ask “what should the client see?” and “who recovers?” without reading every line first.

## How to explain a retry budget

Suppose there are at most three attempts and delays of one and two recorded time units. The maximum number of dependency calls is three and the deliberate waiting is bounded by three units, plus the dependency's own deadline. A real system must include network and queue budgets too. The point is that a client can reason about worst-case waiting. An unbounded `while True` cannot make that promise, even if it usually succeeds quickly.
