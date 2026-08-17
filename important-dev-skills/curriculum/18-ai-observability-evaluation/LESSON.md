# Observability and evaluation for AI workflows

## What you will learn

You will define success before running an experiment, capture a useful redacted trace, compare a baseline and candidate on synthetic cases, and make a release decision tied to evidence.

## Why “it feels better” is not an evaluation

AI output varies and quality has multiple dimensions. A candidate prompt may improve answerable questions while making denied cases leak information or doubling cost. **Evaluation** is a repeatable measurement of defined tasks. **Observability** is the information that lets you understand a run after it happens. You need both: evaluation tells you whether a change helped; traces help explain why.

## Vocabulary

- **Task success:** an explicit rule for what counts as correct for one case type.
- **Failure taxonomy:** a set of named failure categories.
- **Dataset version:** an immutable label for the cases and expected outcomes.
- **Slice:** a meaningful subset, such as unanswerable or access-denied cases.
- **Trace:** a correlated record of one workflow run.
- **Span:** a timed child operation inside a trace, such as retrieval or tool call.
- **Outcome:** final success/failure and reason.
- **Evaluator:** code or process that scores an output against expectations.
- **Model judge:** a model asked to grade another output using a rubric.
- **Rubric:** explicit scoring rules.
- **Calibration:** checking judge scores against human-reviewed examples.
- **Regression gate:** a threshold that blocks release when a metric worsens.
- **Cardinality:** the number of distinct values in a field; unbounded values make systems expensive.
- **Redaction:** removing or masking sensitive content before storage.
- **Rate/percentile:** a proportion / a value such as p95 below which 95% of observations fall.

## Define success and failures first

An answerable question may require the expected policy phrase and a real citation. An unanswerable question succeeds when the assistant abstains. An access-denied case succeeds when it denies without revealing restricted text. Write these rules before selecting a prompt or metric.

A useful failure taxonomy names causes: unsupported claim, wrong citation, policy denial error, tool error, timeout, invalid output, cost/latency breach, and privacy/guardrail failure. “Bad” is too vague to diagnose.

## Mental model: versioned run → trace → score → decision

```text
dataset + config + evaluator versions
        → workflow run → correlated redacted trace
        → deterministic checks + optional judge rubric
        → aggregate + slice comparison → gate → release/hold/rollback
```

Change one variable at a time. Preserve raw outputs locally so a score can be audited. The candidate must run against the same cases and evaluator version as the baseline.

## Trace design

A trace ID connects spans. A model span can record model/prompt version, timing, token counts, and estimated cost. A retrieval span records index version and IDs, not raw restricted text. A tool span records tool name, authorization result, and duration. An outcome span records status and failure category. Redact prompts and content; use a stable hash or short approved ID for correlation. Avoid putting user text in a metric label: that creates high cardinality and privacy risk.

## Deterministic checks versus judges

Code should check schema, access, citation mapping, prohibited claims, and tool authorization. A model judge may assess a nuanced explanation with a rubric, but it can be biased, inconsistent, or persuaded by fluent text. Calibrate it on human-reviewed synthetic examples and include `cannot_decide` and disagreement. A judge score can never override a deterministic privacy or authorization failure.

### A beginner's calibration exercise

Start with a handful of synthetic examples that a person has labeled. For each example, write the expected label and the reason. Give the same examples to the judge using a short rubric such as: “good” means the answer addresses the question and cites an eligible passage; “bad” means it makes an unsupported claim; “cannot_decide” means the evidence is ambiguous. Compare judge labels with human labels and keep disagreements instead of silently choosing the judge's answer.

Calibration does not prove that the judge is correct everywhere. It reveals obvious rubric ambiguity and systematic disagreement on a known sample. If a judge calls an unauthorized answer “good” because it sounds helpful, the deterministic access check must still fail the case. Use the judge for a bounded quality dimension, not as the owner of security or correctness policy.

## Rates, slices, and sample size

Success rate is successes divided by cases. p95 latency is useful for tail experience. Report counts alongside rates: 1/1 (100%) is not strong evidence. Compare slices, not only the aggregate. A candidate that rises from 80% to 83% overall but drops denied cases from 100% to 70% should be held. State that a small synthetic dataset gives uncertain estimates; do not invent confidence.

### What a slice tells you

Suppose there are 100 answerable cases with 90 successes and 10 denied cases with 10 safe denials. Overall success is 100/110, about 91%. If a candidate gets 95/100 answerable cases but only 7/10 denied cases, its overall rate is still 102/110, about 93%, yet it introduced three policy failures. The access-denied slice exposes a risk the aggregate hides. Define slices before running: answerability, access level, language, document freshness, tool use, or cost band can each reveal a different regression.

Sample size changes how confidently you should describe a rate. A result of 1/1 is a useful check that the code path runs, but not evidence that a feature works for a population. With a small synthetic set, report exact counts and say that the estimate is exploratory. More cases and repeated runs can narrow uncertainty; they do not fix a biased dataset or a flawed evaluator.

## Release gates

Write the gate before viewing results. Example: release only if overall task success is not lower than baseline by more than 5 percentage points, no critical privacy/access failure occurs, and p95 latency/cost stays under budget. A gate needs an action: hold rollout, roll back to the baseline config, or investigate a slice. A green aggregate score cannot waive a critical guardrail.

## Reviewing AI-generated instrumentation

AI may suggest logging full prompts, using a judge for authorization, changing the dataset to improve a score, or creating metric labels from user text. Reject those patterns. Verify that span IDs correlate, versions are recorded, redaction happens before storage, and candidate/baseline use identical cases. Ask the AI to look for metric gaming and missing slices, then inspect the data yourself.

## Common mistakes

- Choosing a metric after seeing the preferred result.
- Calling every refusal a failure when some tasks require abstention.
- Letting a judge mark an unauthorized answer correct.
- Reporting percentages without denominators.
- Logging raw prompts or high-cardinality text fields.
- Changing prompt, retriever, model, and evaluator together.
- Releasing on aggregate improvement while a critical slice regresses.

## Knowledge checks

1. What must be defined before running a candidate?
2. Which checks should remain deterministic?
3. Why report counts with rates?
4. What does a release gate do when a critical slice regresses?
5. Why redact content but keep IDs/versions?

### Answers

1. Task success, failure taxonomy, dataset/config/evaluator versions, and the hypothesis.
2. Schema, authorization/access, privacy/guardrails, and citation mapping; a judge cannot safely replace them.
3. A rate from one case is unstable; denominators show sample size.
4. Hold or roll back even if aggregate quality improves.
5. Redaction protects data while IDs and versions preserve correlation and reproducibility.

## Notebook preparation

Run [lab.ipynb](lab.ipynb) from a fresh Python 3 kernel. The harness uses five synthetic cases and an in-memory trace sink. It imports only standard-library modules and writes no files.

## Summary

Trustworthy AI delivery is a measurement loop: define success, version inputs, trace the workflow, score deterministic guardrails and calibrated judgments, inspect slices, and gate release. The course ends here, but the habit continues: evidence should be reproducible, bounded, and safe.
