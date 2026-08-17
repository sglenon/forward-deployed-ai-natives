# Module 18: AI observability and evaluation

## Start here

This final module teaches you to decide whether an AI workflow change is safe to release. You will run a fake policy assistant over a versioned synthetic dataset, collect redacted traces, evaluate deterministic guardrails, compare baseline/candidate slices, and make a release/hold decision. There are no live providers or production conversations.

Prerequisite: [Module 17](../17-rag-retrieval/README.md) and the earlier course modules on tests, logs, traces, privacy, tools, and retrieval. Read [LESSON.md](LESSON.md), then run [lab.ipynb](lab.ipynb).

## Learning goals

- define task success and a useful failure taxonomy;
- capture model, retrieval, tool, timing, token, cost, and outcome metadata in correlated spans;
- separate deterministic evaluators from a model-judge rubric and calibration;
- compare baseline and candidate by slices, rates, and sample-size caveats;
- set a regression gate and release/hold/rollback decision;
- redact content and control trace cardinality/privacy.

## Vocabulary preview

The [lesson](LESSON.md) explains each evaluation term with a concrete example:

- **Slice:** a meaningful subset of cases, such as unanswerable or denied requests.
- **Trace:** a correlated record of one workflow run.
- **Span:** a timed child operation inside a trace.
- **Evaluator:** code or a process that scores an output against expectations.
- **Judge:** a model asked to assess an output using a rubric.
- **Calibration:** comparing judge labels with human-reviewed examples.
- **Regression gate:** a threshold that blocks release when a result worsens.

## Study order (90–150 minutes)

Read the lesson (45–60 min), run the baseline/candidate harness and predictions (45–65 min), then complete the release decision and evidence handoff (10–20 min).

## Completion checklist

- [ ] I defined success for answerable, unanswerable, and denied cases before measuring.
- [ ] I can correlate a redacted trace across model/retrieval/tool/outcome spans.
- [ ] Deterministic guardrails cannot be overruled by a judge score.
- [ ] I reported aggregate and slice rates with sample-size caveats.
- [ ] My release gate has a material regression threshold and rollback action.
- [ ] I can reproduce the decision from dataset/evaluator/config versions.

## Evidence and pass conditions

Keep dataset/config/evaluator versions, raw outputs, traces, failure labels, slice metrics, judge rubric/calibration notes, AI diff review, and release recommendation. Pass means important failure paths and slices are present; privacy/schema/access checks are deterministic; judge disagreement is visible; traces are useful but redacted; and aggregate gains cannot hide a critical regression. This fake harness does not prove production quality or real user outcomes.

## Course conclusion

You have finished the 18-module course when you can explain and reproduce this decision. Continue learning by applying the same evidence boundaries to a small, approved project.
