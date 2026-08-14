# Module 18: AI observability and evaluation

## Outcome

Detect an AI-system regression by tracing model and tool behavior against a versioned evaluation dataset and task-success measure.

## Lab progression

1. Define the user task and failure taxonomy before choosing metrics.
2. Build a small representative dataset with expected outcomes and important slices.
3. Capture model, prompt, retrieval, tool, latency, token, cost, and outcome metadata.
4. Add deterministic checks before model-based grading.
5. Calibrate an LLM judge against human-reviewed examples and record disagreement.
6. Change a prompt, model, or retrieval setting and compare it with the baseline.
7. Gate deployment on material regressions and inspect slice-level failures.
8. Add sampled production feedback without treating unreviewed feedback as ground truth.

## Required evidence

- Versioned dataset, evaluator, prompt, model, and tool configuration.
- Baseline and candidate results with confidence limits or sample-size caveats.
- Trace examples for at least one success and each important failure class.
- A release recommendation tied to task success, guardrails, cost, and latency.

## Pass conditions

- Evaluation cases represent the intended operation rather than only happy paths.
- Deterministic checks are not delegated to an LLM judge.
- Judge bias and disagreement are visible.
- Aggregate improvement cannot hide a critical slice regression.
- Every released result can be traced to its complete version set.
