# Module 9: Async processing, queues, and background jobs

## Start here

An asynchronous job lets a request say “accepted” before slow work finishes. You will model a report queue entirely in memory and learn to survive duplicates, crashes, retries, and cancellation without promising impossible exactly-once execution.

Assume Modules 1–8: functions, persistence boundaries, HTTP outcomes, errors, queues, and tests. [LESSON.md](LESSON.md) introduces `async`/`await`; no server or cloud queue is needed.

## Vocabulary preview

- **Producer:** creates and submits a job.
- **Worker/consumer:** takes a job and performs its operation.
- **Acknowledgement:** tells a queue that delivery is finished.
- **At-least-once delivery:** a job may arrive more than once.
- **Idempotent effect:** repeating an operation does not duplicate its business result.
- **Outbox:** durable unsent work found by reconciliation after a crash.
- **Dead letter:** visible holding state for poison or exhausted jobs.
- **Backpressure:** slowing or rejecting producers when capacity is full.

## What you will know and do

- distinguish synchronous work from asynchronous work and accepted from completed;
- model durable states, acknowledgement order, and crash windows;
- make an effect idempotent and bound retries;
- handle replay, cancellation, and overload honestly.

## Study order and time

Read [LESSON.md](LESSON.md), write predictions, then run [lab.ipynb](lab.ipynb) top-to-bottom in a fresh kernel. The simulation uses deterministic steps rather than real sleeping.

## Completion checklist

- [ ] I drew the submit → enqueue → work → status path.
- [ ] I wrote three predictions about a crash or duplicate.
- [ ] I can explain why “accepted” is not “completed.”
- [ ] I demonstrated idempotent effect and late acknowledgement.
- [ ] I bounded retries and recorded a dead-letter job.
- [ ] I documented what the simulation does not prove.

## Evidence and pass conditions

Keep state transcripts for success, duplicate delivery, worker crash, persist-but-not-enqueued recovery, cancellation, retry exhaustion, and unknown-job authorization. Include a state diagram and operator replay note. You pass when accepted jobs cannot be silently lost, duplicate delivery does not duplicate the chosen effect, retries are bounded, failed work stays visible, and every crash boundary is explainable.

## Next module

Continue to [Module 10: Logging, monitoring, and tracing](../10-logging-monitoring-tracing/README.md), which makes these state transitions diagnosable.

Previous: [Module 8: Testing production code](../08-testing-production-code/README.md).
