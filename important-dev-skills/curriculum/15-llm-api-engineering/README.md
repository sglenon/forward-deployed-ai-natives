# Module 15: LLM API engineering

## Outcome

Integrate a model API with explicit output, latency, rate-limit, token, cost, and failure boundaries.

## Lab progression

1. Implement one narrow text transformation with a fixed success criterion.
2. Record model, prompt, parameters, and client-library version.
3. Require a structured output schema and handle refusal or invalid output.
4. Add streaming only if it improves the user flow, then handle interruption.
5. Bound request time, input size, output tokens, retries, and concurrency.
6. Simulate rate limiting, timeout, provider error, and partial stream failure.
7. Measure latency, token use, estimated cost, and task success separately.
8. Define fallback behavior that does not misrepresent failure as an answer.

## Required evidence

- A versioned input/output contract and representative test set.
- Failure tests using a fake provider boundary.
- Cost and latency measurements for the test set.
- A data-handling note covering what may be sent to the provider.

## Pass conditions

- Invalid structured output cannot silently enter downstream logic.
- Retries are bounded and respect provider guidance.
- Streaming cancellation releases resources.
- Cost and latency limits are enforceable.
- Provider failure is visible to the user and operator.
