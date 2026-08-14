# Important Dev Skills

An industry-ready developer curriculum for engineers who work with AI-generated code but must still understand, review, debug, and own the system.

The curriculum builds individual engineering skills through focused exercises. Modules 1–14 cover production software foundations. Modules 15–18 extend those foundations into AI engineering.

The detailed topic inventory is maintained in [00-important-dev-skills-list.md](00-important-dev-skills-list.md). The module pages below define the exercises, evidence, and pass conditions.

## Core curriculum


| Module | Lab                                                                                                | What the learner proves                                           |
| ------: | -------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| 1      | [Code structure and maintainability](curriculum/01-code-structure-maintainability/README.md)       | Refactor safely and reject unnecessary abstraction                |
| 2      | [HTTP and API design](curriculum/02-http-api-design/README.md)                                     | Design a predictable, compatible HTTP contract                    |
| 3      | [Authentication and authorization](curriculum/03-authentication-authorization/README.md)           | Enforce identity, role, permission, and ownership rules           |
| 4      | [API validation and data contracts](curriculum/04-api-validation-data-contracts/README.md)         | Make invalid inputs explicit and responses stable                 |
| 5      | [SQL and schema design](curriculum/05-sql-schema-design/README.md)                                 | Model relationships and integrity in the database                 |
| 6      | [Database performance and transactions](curriculum/06-database-performance-transactions/README.md) | Diagnose query cost and protect concurrent changes                |
| 7      | [Error handling and resilience](curriculum/07-error-handling-resilience/README.md)                 | Handle failure without leaking, hanging, or duplicating work      |
| 8      | [Testing production code](curriculum/08-testing-production-code/README.md)                         | Prove behavior and expose false confidence from AI-generated code |
| 9      | [Async processing and queues](curriculum/09-async-queues-background-jobs/README.md)                | Move slow work safely into a recoverable worker flow              |
| 10     | [Logging, monitoring, and tracing](curriculum/10-logging-monitoring-tracing/README.md)             | Diagnose a failure from correlated telemetry                      |
| 11     | [Security for developers](curriculum/11-security-for-developers/README.md)                         | Reproduce and fix common application vulnerabilities              |
| 12     | [Docker, environments, and CI/CD](curriculum/12-docker-environments-cicd/README.md)                | Build a repeatable path from change to rollback                   |
| 13     | [Scalability and production system design](curriculum/13-scalability-system-design/README.md)      | Identify the next realistic bottleneck using evidence             |
| 14     | [Debugging and AI-generated code review](curriculum/14-debugging-ai-code-review/README.md)         | Find the root cause and verify an AI-proposed fix                 |


## AI engineering extension

Begin this extension after the core curriculum. It assumes the learner can already build, secure, test, observe, and operate a conventional service.


| Module | Lab                                                                                            | What the learner proves                                  |
| ------: | ---------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| 15     | [LLM API engineering](curriculum/15-llm-api-engineering/README.md)                             | Bound model cost, latency, output, and failure behavior  |
| 16     | [Tool calling and agent architecture](curriculum/16-tool-calling-agent-architecture/README.md) | Build a permissioned, terminating, recoverable tool loop |
| 17     | [RAG and retrieval](curriculum/17-rag-retrieval/README.md)                                     | Diagnose retrieval separately from generation            |
| 18     | [AI observability and evaluation](curriculum/18-ai-observability-evaluation/README.md)         | Detect regressions with versioned traces and evals       |


## Standard lab method

Every lab follows the same evidence loop:

1. Establish the baseline.
2. Reproduce the failure or limitation.
3. State a hypothesis before changing code.
4. Make one bounded improvement.
5. Run positive, negative, and failure-path checks.
6. Review the diff, including AI-generated changes.
7. Record what the evidence proves and does not prove.

Passing code is necessary but not sufficient. A learner must explain the behavior, defend the tradeoff, and show evidence another engineer can reproduce.

## Delivery model

- Complete modules in order unless a diagnostic assessment supports skipping one.
- Allow 90–150 minutes for each foundation lab.
- Pair each implementation with a short adversarial review.
- Use synthetic data and local-only attack exercises.
- Repeat selected exercises in a real repository only under its access and data rules.
- Require mentor review at Modules 4, 8, 12, 14, and 18.

AI coding tools are allowed throughout. Learners must record the request given to the tool, inspect the generated diff, verify referenced APIs, and reject changes they cannot explain.

## Inspiration

The progressive “working but incomplete, then improve one property at a time” format is inspired by [johnoffshorly/dev-skills-lab](https://github.com/johnoffshorly/dev-skills-lab). The curriculum structure and evidence model here are original to this program.