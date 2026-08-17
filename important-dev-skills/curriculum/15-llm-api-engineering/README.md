# Module 15: Engineering a safe LLM API boundary

## Start here

You will build a fake provider adapter for classifying synthetic support tickets. The fake provider is deterministic, local, and free. It lets you learn contracts, validation, deadlines, retries, streaming, privacy, and cost limits without an account or a live model.

You should know functions, exceptions, JSON-like dictionaries, tests, retries, and logs from [Module 14](../14-debugging-ai-code-review/README.md). Read [LESSON.md](LESSON.md) before opening [lab.ipynb](lab.ipynb).

## Learning goals

- explain model, prompt, parameter, provider, and version;
- enforce a structured output schema and handle refusal or malformed output;
- bound input/output size, deadline, rate, concurrency, retries, and estimated cost;
- model deterministic streaming and cancellation without treating partial output as success;
- keep provider-specific details behind a replaceable boundary and protect private data;
- review AI-generated client options and fallback code critically.

## Vocabulary preview

The [lesson](LESSON.md) introduces each term with a small example:

- **Adapter:** a wrapper that gives application code a stable interface to a provider.
- **Schema:** rules describing required fields, types, and allowed values.
- **Structured output:** model output with a predictable data shape.
- **Refusal:** a response that declines instead of producing the requested result.
- **Token:** a rough unit of text used to track usage and cost.
- **Deadline:** the latest time an operation may finish.
- **Streaming:** receiving a response in chunks over time.

## Study order (90–150 minutes)

Read the lesson (40–55 min), run the notebook predictions and fake adapter (45–65 min), then finish the challenge and evidence handoff (10–20 min). Restart the kernel and run all cells before claiming completion.

## Completion checklist

- [ ] I can state the versioned input/output contract and reject invalid model output.
- [ ] I tested empty/oversized input, refusal, timeout, rate limit, provider error, and cancellation.
- [ ] I can calculate estimated cost using the notebook's labeled placeholder table.
- [ ] I know which failures are retryable and why retries are bounded.
- [ ] Business logic depends on the adapter contract, not a provider SDK.
- [ ] I reviewed an AI-style diff for invented options, secret logging, and silent fallbacks.

## Evidence and pass conditions

Keep contract/version notes, fake-provider outputs, failure traces, retry/attempt counts, latency and token calculations, and your AI diff review. Pass means malformed/refused/partial output cannot reach business logic; limits are enforceable; cancellation is visible; errors are safe for users and useful to operators; and a provider can be swapped without changing ticket logic. This local fake cannot prove real model quality, live pricing, or network behavior.

## Next module

Continue to [Module 16: Tool calling and agent architecture](../16-tool-calling-agent-architecture/README.md).
