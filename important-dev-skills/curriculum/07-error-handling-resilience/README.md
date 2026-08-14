# Module 7: Error handling and resilience

## Outcome

Make an application respond safely and predictably to invalid input, unavailable dependencies, timeouts, and unexpected defects.

## Lab progression

1. Classify expected domain, validation, dependency, and unexpected errors.
2. Replace scattered catch blocks with explicit propagation and a central boundary.
3. Return safe client errors while preserving diagnostic context internally.
4. Add deadlines to outbound calls.
5. Retry only classified transient failures and use bounded exponential backoff with jitter.
6. Make replay safe with idempotency where required.
7. Add a circuit breaker or graceful degradation only where the user flow has a safe fallback.
8. Exercise shutdown while requests or jobs are in flight.

## Required evidence

- A failure matrix with user effect, retry rule, recovery path, and owner.
- Deterministic tests for timeout, transient failure, permanent failure, and unexpected defect.
- Evidence that client responses do not expose stack traces or secrets.
- One recovery drill after repeated dependency failure.

## Pass conditions

- Expected and unexpected errors remain distinguishable.
- Retries are bounded, observable, and replay-safe.
- The application does not hang indefinitely on a dependency.
- Degraded behavior is explicit rather than silent corruption.
- An operator can determine what happens next.
