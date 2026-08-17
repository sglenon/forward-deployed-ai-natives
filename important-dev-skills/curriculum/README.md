# Important Dev Skills: study guide

This directory is a self-study course for developers who use AI coding tools and still want to understand, test, and own the code they ship. It is designed for a curious junior developer. You do not need to know every word in advance: each module introduces its vocabulary before asking you to use it.

## What you need

- Python 3.10 or newer. Check with `python3 --version` (on Windows, `py --version` may be the equivalent).
- A text editor or IDE.
- A terminal for running small commands.
- A way to open Jupyter notebooks. You may use an existing Jupyter installation, VS Code's notebook support, JupyterLab, or another local notebook viewer. This curriculum does not assume that Jupyter is installed or prescribe one installation method.

If you need to install a tool, follow the official instructions for your operating system and your team's policy. The exercises use Python's standard library and synthetic data, so they do not require cloud accounts, API keys, or a network connection.

## How a module is organized

Each module has three files:

1. `README.md` is the landing page. It tells you where to start, what you will learn, and what evidence to collect.
2. `LESSON.md` is the study chapter. Read it slowly; it explains the ideas, vocabulary, examples, and decisions behind the lab.
3. `lab.ipynb` is the interactive notebook. Run its cells in order, predict what will happen before executing prediction exercises, and edit the marked TODOs.

The lesson is the explanation, and the notebook is the practice space. A notebook is not a magic environment: it is a sequence of text and Python cells that share variables while the notebook is running.

## Recommended study workflow

For each module:

1. Read the module `README.md` and note any prerequisite you do not recognize.
2. Read `LESSON.md` through the first knowledge check. Write your own answers before looking at the answer section.
3. Open `lab.ipynb` in your local notebook tool. Run the environment check, then continue top-to-bottom.
4. Stop at every “Predict” prompt. Write a prediction in the markdown cell or in your notes before running the next code cell.
5. Attempt each TODO and independent challenge for at least 10 minutes before opening its reference solution.
6. Run the complete notebook from a fresh kernel. A successful run is evidence that the examples work, not proof that you understand them.
7. Complete the module checklist and save the responsibility map, hypothesis, test output, and AI review notes requested by the module.
8. Explain one idea aloud or in writing as if teaching a teammate. If you cannot explain a change, pause and investigate it.

Most modules take 90–150 minutes. It is fine to split a module across days; record where you stopped so that a fresh-kernel run remains part of your final check.

## How solutions work

The notebooks deliberately put explanations and reference solutions after the attempt. Solution cells are still executable, so the whole notebook can be run from a fresh namespace. Try first, then reveal the solution and compare your approach with it. There may be more than one correct implementation; the reference solution demonstrates one small, explainable choice and includes assertions that make its behavior visible.

Do not delete a failing assertion just to make a notebook run. Instead, read the message, compare it with the lesson, and correct the code or your expectation. If you make an exploratory copy, keep the original lab clean so that you can reproduce it later.

## A safe local-only rule

Treat every exercise as disposable local training data. Use synthetic names and records only. Do not paste credentials, customer information, private source code, or production logs into a notebook or AI tool. Do not add network calls, real databases, cloud queues, destructive shell commands, or writes outside the notebook's working area. If an existing project has a command that points outside the lab, stop and ask a mentor before running it.

## Using AI as a learning partner

AI tools are allowed, but the goal is understanding rather than accepting a plausible answer.

- Ask for a concept explanation, a small hint, or possible risks before asking for a complete implementation.
- Save the prompt and the response when the module asks for AI evidence.
- Read every generated line. Verify that names and APIs exist in the local code and that errors are still handled.
- Ask the tool to explain a diff in plain language, then check that explanation yourself.
- Reject generated code you cannot explain. More classes, wrappers, configuration, or “future-proof” abstractions are not automatically better.
- Never send secrets or private data to an AI service.

## Troubleshooting notebooks

If a cell fails:

- Read the full traceback. The last line usually names the immediate problem; look upward for the file and line that caused it.
- Check that you ran cells in order and that you did not accidentally overwrite a variable.
- Restart the kernel and run all cells again. A notebook that only works after an unusual execution order is not reliable.
- Compare your edits with the lesson's syntax examples. Common beginner issues include missing quotes, incorrect indentation, and confusing a function call (`work()`) with the function itself (`work`).
- Confirm that your Python version is 3.10 or newer.
- If the failure is in a solution or baseline cell, keep the error message and report it rather than silently changing the assertion.

## The 18-module sequence

Complete the foundation modules in order. The AI engineering extension assumes that you understand the earlier software and testing habits.

### Foundation

1. [Code structure and maintainability](01-code-structure-maintainability/README.md) — understand responsibilities, refactor safely, and resist unnecessary abstraction.
2. [HTTP and API design](02-http-api-design/README.md) — design predictable, compatible requests and responses.
3. [Authentication and authorization](03-authentication-authorization/README.md) — distinguish identity, roles, permissions, and ownership.
4. [API validation and data contracts](04-api-validation-data-contracts/README.md) — make invalid input explicit and responses stable.
5. [SQL and schema design](05-sql-schema-design/README.md) — model relationships and integrity in a database.
6. [Database performance and transactions](06-database-performance-transactions/README.md) — measure query cost and protect concurrent changes.
7. [Error handling and resilience](07-error-handling-resilience/README.md) — handle failure without leaking, hanging, or repeating work.
8. [Testing production code](08-testing-production-code/README.md) — prove behavior and detect false confidence from generated code.
9. [Async processing and queues](09-async-queues-background-jobs/README.md) — move slow work into a recoverable worker flow.
10. [Logging, monitoring, and tracing](10-logging-monitoring-tracing/README.md) — diagnose a failure from correlated telemetry.
11. [Security for developers](11-security-for-developers/README.md) — reproduce and fix common application vulnerabilities locally.
12. [Docker, environments, and CI/CD](12-docker-environments-cicd/README.md) — build a repeatable path from change to rollback.
13. [Scalability and production system design](13-scalability-system-design/README.md) — identify the next realistic bottleneck using evidence.
14. [Debugging and AI-generated code review](14-debugging-ai-code-review/README.md) — find root causes and verify AI-proposed fixes.

### AI engineering extension

Start this extension after the foundation, or after a mentor confirms that you have the required background.

15. [LLM API engineering](15-llm-api-engineering/README.md) — bound model cost, latency, output, and failure behavior.
16. [Tool calling and agent architecture](16-tool-calling-agent-architecture/README.md) — build a permissioned, terminating, recoverable tool loop.
17. [RAG and retrieval](17-rag-retrieval/README.md) — diagnose retrieval separately from generation.
18. [AI observability and evaluation](18-ai-observability-evaluation/README.md) — detect regressions with versioned traces and evaluations.

Every module uses the same evidence loop: establish a baseline, reproduce behavior, write a hypothesis, make one bounded change, test positive/negative/failure paths, inspect the diff, and record what the evidence does and does not prove.
