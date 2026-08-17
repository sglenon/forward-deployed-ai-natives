# Building a reliable model-provider boundary

## What you will learn

You will wrap a deterministic fake model behind a small adapter, validate structured ticket classifications, and make failure and cost limits explicit. The same design applies whether a future provider is a local model or a hosted API.

## Why an LLM call is not an ordinary function

A normal function usually returns the type its author chose. A language model produces text by prediction, so it can omit fields, refuse, exceed limits, or return a plausible but invalid value. A network provider can also time out or rate-limit you. Treat the model as an unreliable dependency at a boundary, not as a trusted parser.

## Vocabulary

- **Model:** the trained system that produces a response.
- **Provider:** the service or library that runs a model.
- **Model identifier/version:** a name and revision that make behavior reproducible.
- **Prompt:** instructions and input sent to the model.
- **Parameter:** a setting such as temperature or maximum output tokens.
- **Adapter:** a small provider-neutral wrapper exposing the contract your application needs.
- **Structured output:** data with a defined shape, such as a dictionary with four fields.
- **Schema:** rules describing required fields, types, and allowed values.
- **Refusal:** a response that declines the request rather than producing the task result.
- **Token:** a rough unit of text used for usage and cost accounting.
- **Deadline:** the latest time an operation is allowed to finish.
- **Rate limit:** a maximum number of requests in a time window.
- **Retryable/non-retryable:** a failure that may succeed if repeated / one that repetition cannot fix.
- **Streaming:** receiving response chunks over time instead of one complete response.
- **Cancellation:** a caller's request to stop work that is no longer needed.
- **Provider-neutral:** business code does not import provider-specific names.

## Mental model: application → adapter → provider

```text
ticket text → validate/limit → adapter contract → fake provider
                         ← typed result or typed failure
```

Only the adapter knows provider request fields. The ticket service knows that classification returns `category`, `urgency`, `summary`, and `confidence`. This separation lets tests use a fake and lets a future provider change without rewriting business rules.

## The contract before the client

Write the contract first. A ticket has bounded text. A successful result has:

```text
category: billing | access | technical | other
urgency: low | medium | high
summary: non-empty string, at most 120 characters
confidence: number from 0 through 1
```

Version the contract (`ticket-v1`) and prompt template (`triage-prompt-v1`). A version is a label for the exact assumptions used in an experiment. Keep model ID, adapter version, parameters, and client version in traces.

In Python, dictionaries represent JSON-like objects. A validation function should return a safe result or a clear failure rather than letting an invalid object reach downstream logic. Unknown enum values and extra fields should have an explicit policy; strict validation is easier to reason about in a small exercise.

## Input and output bounds

The adapter should reject empty text and truncate or reject oversized text according to product policy. A maximum output-token setting is a provider hint, not proof that the response obeys it, so validate the actual summary length too. Record input characters, output characters, and usage tokens. Do not log full ticket text by default; use a redacted ID or hash.

## Failure classes and retries

Classify failures before choosing retry behavior:

| Failure | Retry? | Reason |
| --- | --- | --- |
| malformed model output | no | repeating the same request may repeat the defect; validate or revise contract |
| refusal | usually no | it is a policy/result decision, not transport noise |
| timeout | bounded yes | a short retry may recover, but deadline still wins |
| rate limit | bounded later | respect a retry-after/backoff signal |
| authentication or bad request | no | code/configuration must change |
| transient provider outage | bounded yes | do not turn one ticket into an unbounded loop |

An **attempt** is one provider call. Keep a maximum attempts count and one overall deadline. A nested timeout must never allow work past the caller's deadline. Exponential backoff is increasing wait time; the notebook uses deterministic short waits so it stays fast.

## Structured results and typed failures

Return an application result with either a validated classification or a failure reason such as `invalid_output`, `refused`, `deadline`, `rate_limited`, or `provider_error`. Keep user-safe text separate from operator detail. Never silently turn a refusal into a guessed category. A partial stream is not a successful structured record.

## Streaming and cancellation

Streaming can improve perceived latency when users need text as it arrives. The trade-off is cleanup and incomplete output. A stream is an iterator of chunks; cancellation tells the provider and caller to stop. The notebook simulates chunks and raises a cancellation exception at a deterministic index. The final validator must reject a partial summary unless the product explicitly supports drafts.

## Cost and privacy

Estimated cost is a calculation, not a bill. Use a versioned placeholder table:

```text
triage-fake-v1: input 0.001 units/token, output 0.002 units/token
```

Record the table version and formula. State sample-size limits; three fake calls cannot predict production price or quality. Send only approved data. Synthetic tickets are safe for this lab; real personal data, secrets, and unreviewed prompts are not.

## Reviewing AI-generated integration code

Ask for a provider-neutral interface and a bounded diff. Check every client option against the installed version. Watch for invented `timeout_seconds`, unlimited retries, logging of authorization headers or prompts, parsing with `eval`, silent “fallback” classifications, and business code importing a provider SDK. Ask which failures are safe to retry and where the authoritative deadline lives. Run the fake failure matrix yourself.

## Common mistakes

- Treating a JSON-looking string as validated structured output.
- Retrying malformed output or a non-idempotent downstream write.
- Setting a timeout on one nested call but not the complete operation.
- Counting a partial stream as a successful answer.
- Reporting fake placeholder prices as live pricing.
- Logging raw ticket text to make debugging convenient.
- Building provider-specific behavior into every caller.

## Knowledge checks — pause before answers

1. Why does a max-output parameter not replace schema validation?
2. Which failure should not be retried: malformed JSON or a short transient outage? Why?
3. What belongs in an adapter rather than ticket business logic?
4. Why is a partial stream not a valid classification?
5. What does a cost table version allow you to reproduce?

### Answers

1. It is a request hint; the provider may ignore it or produce a different shape. Validate actual output.
2. Malformed JSON should not be blindly retried; an outage may be retried a bounded number of times before the deadline.
3. Provider request/response mapping, timeout/retry mechanics, and usage extraction; business code should consume the stable result.
4. Required fields may be missing or truncated, so downstream code could make a false decision.
5. It records which assumptions and rates produced an estimate; it does not turn fake rates into live billing data.

## Notebook preparation

Open [lab.ipynb](lab.ipynb), restart the kernel, and run top-to-bottom. It uses a fake provider with modes for success, malformed output, refusal, timeout, rate limit, and streaming cancellation. No network, secrets, third-party packages, or file writes are used.

## Summary and next connection

Reliable LLM integration starts with a versioned contract and an adapter that makes uncertainty measurable: validate output, classify failures, bound work, protect data, and report cost honestly. Module 16 uses the same boundary idea for tool calls, where invalid model output can cause state-changing actions.
