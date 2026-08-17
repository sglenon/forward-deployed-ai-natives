# Module 7: Error handling and resilience

## Start here

An error is a fact that an operation did not complete as promised. **Resilience** is designing what happens next without hiding failure or doing unsafe duplicate work. With deterministic fake dependencies, clocks, and sleepers, you will classify errors, centralize the boundary, bound attempts/deadlines, use idempotency, and model honest degradation. The lab never performs real sleeps or network calls.

You should know exceptions, HTTP response dictionaries, and Module 2's API contract. All dependencies and data are local and synthetic.

## Vocabulary preview

- **Transient failure:** a problem that may succeed if tried later.
- **Permanent failure:** a problem that retrying the same input will not fix.
- **Deadline:** the latest time an operation is allowed to finish.
- **Retry:** repeating a failed operation under a bounded policy.
- **Backoff:** increasing the delay between retry attempts.
- **Idempotency key:** an identity that lets a repeated write reuse its original result.
- **Circuit breaker:** a state machine that temporarily stops calls to a failing dependency.

The full [lesson](LESSON.md) builds a failure matrix before introducing retry logic.

## What you will know and do

- distinguish validation/domain, transient, permanent, timeout, cancellation, and unexpected defects;
- propagate expected failures to one boundary while returning safe client messages and useful internal evidence;
- design deadlines, classified bounded retries/backoff/jitter, and idempotent writes;
- model a circuit breaker or truthful queue/fallback and explain shutdown/cancellation;
- review AI code for catch-all exceptions, infinite retries, fake success, leaked internals, and non-replay-safe work.

## Study order and time

Read [LESSON.md](LESSON.md) and complete the failure matrix before running [lab.ipynb](lab.ipynb). Plan 90–150 minutes. Restart the kernel before the final run.

## Completion checklist

- [ ] I captured baseline and final status, safe body, attempts, side effects, and correlation ID.
- [ ] I wrote hypotheses before changing code.
- [ ] I tested invalid, transient, permanent, timeout, exhaustion, duplicate, cancellation, and unexpected defect paths.
- [ ] Every retry is classified, bounded, visible, and replay-safe.
- [ ] No response exposes stack traces, secrets, SQL, or dependency bodies.
- [ ] I can explain what an honest fallback promises and what remains unresolved.

## Evidence and pass conditions

Keep the failure matrix, hypothesis log, deterministic tests, annotated diff, and recovery drill. Pass means expected/unexpected errors stay distinguishable; dependency calls have bounded deadlines/retries; repeated requests do not duplicate the effect; degradation is truthful; and local evidence is not presented as exactly-once or production capacity.

## Next module

Continue to [Module 8: Testing production code](../08-testing-production-code/README.md), applying these contracts with a broader test strategy.
