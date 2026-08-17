# Module 16: Tool calling and agent architecture

## Start here

You will build a deterministic order-support loop with a fake model and two local tools. The exercise teaches how to validate calls, separate model text from authorization, require confirmation for state changes, and stop/recover predictably. Nothing touches real accounts, payments, shells, or networks.

Prerequisite: [Module 15](../15-llm-api-engineering/README.md), plus basic dictionaries, exceptions, tests, and idempotency. Read [LESSON.md](LESSON.md), then work through [lab.ipynb](lab.ipynb).

## Learning goals

- define tool schemas, registrations, calls, results, and loop state;
- validate tool names and arguments before implementation code runs;
- enforce authorization and confirmation in code, independent of model text;
- bound steps and deadlines and classify termination reasons;
- make state-changing retries idempotent and reason about replay/resume;
- recognize prompt injection and compare an agent with a deterministic workflow.

## Vocabulary preview

The [lesson](LESSON.md) explains these terms before the lab uses them:

- **Tool call:** a model request naming an approved tool and its arguments.
- **Tool result:** the bounded value returned by a tool.
- **Registry:** an allow-list of tool names and implementations.
- **Authority:** trusted permission to act on a specific resource.
- **Confirmation gate:** an independent approval required before a risky action.
- **Termination reason:** the explicit explanation for why a loop stopped.
- **Replay/resume:** continuing safely from saved state after interruption.

## Study order (90–150 minutes)

Read the lesson (45–60 min), run the notebook's model sequences and failure checks (45–65 min), then complete the challenge/evidence handoff (10–20 min).

## Completion checklist

- [ ] Unknown tools and malformed arguments never reach tool code.
- [ ] Cross-user orders and unconfirmed cancellation are denied without mutation.
- [ ] Every run stops with one explicit termination reason.
- [ ] Repeating an approved cancellation does not duplicate its state change.
- [ ] I can explain what state is safe to resume after a crash.
- [ ] I reviewed AI suggestions for prompt-injection and permission bypass.

## Evidence and pass conditions

Keep schemas, registry, state/permission diagram, fake-model sequences, traces for success/denial/tool failure/max steps, and AI review. Pass means model text cannot grant authority or register tools; arguments/results are bounded; stop limits are enforceable; replay is safe; and you can name a deterministic alternative. This local loop does not prove production authorization or distributed durability.

## Next module

Continue to [Module 17: RAG and retrieval](../17-rag-retrieval/README.md).
