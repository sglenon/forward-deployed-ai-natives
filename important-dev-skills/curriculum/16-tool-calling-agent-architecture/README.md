# Module 16: Tool calling and agent architecture

## Outcome

Build a small agent loop that selects typed tools, respects permissions, terminates predictably, and recovers from tool failure.

## Lab progression

1. Define two read-only tools with narrow schemas and deterministic implementations.
2. Validate every model-produced tool call before execution.
3. Add explicit loop state, maximum steps, timeout, and termination reasons.
4. Distinguish model, validation, tool, and policy failures.
5. Add one state-changing tool behind a human confirmation or policy gate.
6. Test repeated calls, invalid arguments, unavailable tools, partial results, and attempted permission bypass.
7. Make replay and resume behavior explicit.
8. Compare a direct deterministic workflow with the agent loop and justify when the agent adds value.

## Required evidence

- Agent-state and permission diagrams.
- Tool schemas plus validation and policy tests.
- Traces for successful, denied, failed, and maximum-step runs.
- A decision note explaining the chosen human gate and termination rules.

## Pass conditions

- Model text alone cannot grant tool authority.
- Invalid calls never reach a tool implementation.
- Every run terminates with a classified reason.
- State-changing retries cannot duplicate effects silently.
- The learner identifies tasks that should remain deterministic code.
