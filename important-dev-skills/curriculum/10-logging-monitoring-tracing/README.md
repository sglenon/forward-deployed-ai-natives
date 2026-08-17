# Module 10: Logging, monitoring, and tracing

## Start here

Telemetry is information a running program emits so people can understand it. You will instrument a local API → store → worker simulation with safe structured events, metrics, traces, and health signals. A fake clock keeps every result deterministic.

Assume Modules 1–9: boundaries, failures, queues, and tests. No vendor, telemetry service, network, or real customer data is used.

## Vocabulary preview

- **Structured log:** an event represented as named fields.
- **Metric/counter:** a numeric measurement; a counter increases for occurrences.
- **Histogram:** samples or buckets showing a distribution such as latency.
- **Trace/span:** one end-to-end journey and one timed operation within it.
- **Correlation ID:** a value connecting events for one request.
- **Cardinality:** the number of distinct values in a field or label.
- **Liveness/readiness:** whether a process runs / should receive traffic.
- **Saturation:** how close a finite resource is to its limit.

## What you will know and do

- distinguish logs, metrics, traces, and health signals;
- propagate IDs across sync and async boundaries;
- measure latency, throughput, errors, and saturation;
- diagnose a seeded delay before reading source;
- define an owned alert and redact sensitive values.

## Study order and time

Read [LESSON.md](LESSON.md), answer checks, then run [lab.ipynb](lab.ipynb) with a fresh kernel. Keep the event timeline and incident note.

## Completion checklist

- [ ] I wrote three predictions about which signal would change.
- [ ] Every event has a correlation ID and safe bounded fields.
- [ ] I can explain a counter versus a histogram and a span.
- [ ] I diagnosed the seeded delay from telemetry first.
- [ ] I separated liveness from readiness.
- [ ] I defined an alert owner, threshold, and action.

## Evidence and pass conditions

Keep successful/failed captures, a redacted event sample, metric definitions, a correlated trace timeline, health results, incident notes, and an AI diff review. You pass when context survives API/store/worker boundaries, metrics avoid unbounded labels, readiness follows documented dependencies, alerts have owners/actions, and no secret or raw payload is emitted.

## Next module

Continue to [Module 11: Security for developers](../11-security-for-developers/README.md). Its threat exercises use the same discipline: define what evidence a signal does and does not provide.

Previous: [Module 9: Async processing, queues, and background jobs](../09-async-queues-background-jobs/README.md).
