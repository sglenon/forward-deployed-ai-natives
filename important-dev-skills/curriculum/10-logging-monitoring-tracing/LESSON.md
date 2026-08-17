# Lesson: make a running program explain itself

## Learning goals

You will emit safe structured events, measure useful signals, propagate context through an async boundary, and diagnose a seeded slow dependency before opening source code.

## Why telemetry matters

**Telemetry** is information emitted by a running system for later diagnosis. A request can be “working” while users experience slow responses. Without context, a pile of text messages cannot tell which store call belongs to which request. AI-generated instrumentation often logs entire payloads, adds labels with one value per user, or reports a process as healthy when its dependency is unavailable.

## Vocabulary

- **Log/event:** one recorded statement about something that happened.
- **Structured log:** an event represented as fields (usually JSON-like data), not one sentence that must be parsed.
- **Log level:** severity such as DEBUG, INFO, WARNING, or ERROR.
- **Metric:** a numeric measurement collected over time.
- **Counter:** a metric that increases for occurrences, such as requests.
- **Histogram:** buckets or samples showing a distribution, such as latency.
- **Cardinality:** number of distinct values in a field; unbounded user IDs make expensive labels.
- **Trace:** one end-to-end journey through components.
- **Span:** one timed operation inside a trace.
- **Correlation/request ID:** a value used to connect events for one request.
- **Liveness:** whether the process can run its basic loop.
- **Readiness:** whether it should receive traffic for its intended workflow.
- **Saturation:** how close a finite resource is to its limit.
- **Alert:** a rule that asks an owner to act when a symptom crosses a threshold.

## Logs, metrics, traces: three questions

Logs answer “what happened?” Metrics answer “how often or how much?” Traces answer “where did this one journey spend time?” Use each for its strength. A counter can show that errors rose, but not which store span was slow. A trace can show one request, but not the rate of all failures.

Every event in this lesson has a timestamp from a fake clock, level, event name, component, correlation ID, outcome, and bounded duration. It omits authorization headers, raw documents, and secret values. A redaction rule is part of the telemetry contract, not an afterthought.

## Context propagation

At ingress, accept a valid synthetic request ID or create one. Pass it as an ordinary argument to the store and worker. A trace ID groups the whole journey; each component creates a new span ID. Do not use one global “current request” variable: two requests would overwrite each other and leak context.

At an async boundary, put the trace ID in the minimal job message. The worker continues the same trace or links a new trace according to policy. The important property is that an operator can connect submission and completion.

## Measuring the four signals

- **Latency:** how long one operation takes. Percentiles (p50, p95, p99) describe a distribution better than one average.
- **Throughput:** completed operations per unit of fake time.
- **Errors:** count or rate of failed outcomes; classify them consistently.
- **Saturation:** queue depth, active workers, or pool usage near a limit.

The notebook uses a deterministic fake clock and a histogram list. No timing assertion depends on the computer running quickly.

## Health is not one boolean

Liveness should stay healthy if the process can serve a health loop; restarting a process because a database is temporarily down can make recovery worse. Readiness asks whether the documented workflow can serve traffic. Dependency health is a separate result naming the dependency and reason. Write the policy first: in this exercise, a store outage makes readiness false but liveness true.

## Worked event and diagnosis

```python
event = {
    "ts": "12.000", "level": "INFO", "name": "store.read",
    "component": "store", "trace_id": "tr-7", "span_id": "sp-2",
    "outcome": "ok", "duration_ms": 4,
}
```

If the API span is 120 ms and the store span is 110 ms, the store is a strong candidate for the delay. This is evidence, not absolute proof: uninstrumented serialization could also consume time. State what the trace shows and what it cannot show.

## Alert ownership

An alert needs a symptom, threshold, window, owner, and action. “Latency is bad” is not actionable. “Page the reports owner when p95 exceeds 200 ms for three fake windows; inspect store saturation and roll back the last query change” is better. Avoid alerting on every individual error or a high-cardinality label.

## AI diff review

For generated telemetry, ask: is each field bounded and safe? Does each metric answer a named question? Are IDs propagated, generated, or accidentally global? Are errors logged once at the boundary? Does the API exist in the checked-out library? Remove raw payloads, unbounded labels, and duplicate noisy events.

## Syntax used in the notebook

`@dataclass` creates simple state holders for the fake clock and telemetry. `field(default_factory=list)` prevents shared event lists. `**fields` collects named event fields into a dictionary. `set(...)` makes a unique collection for a correlation check, while `max(samples)` finds a deterministic worst sample. No wall-clock call is used.

## Common mistakes

1. Logging a whole request, token, or document because it is convenient.
2. Using a global current trace ID that leaks one request into another.
3. Adding one metric label per user or URL and creating unbounded cardinality.
4. Logging the same exception at every layer and drowning out the owner signal.
5. Calling a process live merely because a required dependency is unavailable.

## Knowledge checks — pause before answers

1. What question is a metric better at answering than a log?
2. Why should span IDs differ while a trace ID stays connected?
3. Why can liveness remain true when readiness is false?
4. What is dangerous about a metric label containing a user ID?
5. What makes an alert actionable?

### Answers

1. Metrics summarize rates, counts, distributions, and resource pressure over time; a log gives detail about one event.
2. One trace represents one journey, while spans identify separate timed operations inside it.
3. The process may be alive but unable to serve its workflow because a dependency is down. Restarting cannot necessarily fix the dependency.
4. Distinct user IDs create unbounded cardinality, making storage, queries, and alerts expensive and noisy.
5. It names a symptom, threshold/window, responsible owner, and next action.

## Notebook preparation

Open [lab.ipynb](lab.ipynb) in a fresh kernel. Predict which signal changes before each experiment. The notebook captures local dictionaries rather than sending telemetry anywhere. Save the redacted event sample, metric definitions, trace timeline, and incident note.

## Summary and next connection

Useful telemetry is structured, correlated, bounded, and tied to a question. Logs, metrics, traces, and health checks complement one another. In Module 11 you will apply the same boundary discipline to security: trace untrusted input to a sink and prove a fix with a negative test.
