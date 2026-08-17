# Module 14: Debugging and reviewing AI-generated code

## Start here

This module teaches a repeatable way to find a bug before accepting a proposed fix. You will work on a tiny, local-only note service whose “save twice” bug comes from checking the retry key after writing. The data is synthetic and held in memory; there is no server or database to configure.

You need to be comfortable with functions, dictionaries, tests with `assert`, exceptions, and the request/data flow ideas from [Module 7](../07-error-handling-resilience/README.md). You do not need production incident experience. Every debugging term is introduced in [LESSON.md](LESSON.md).

## What you will learn

- separate an observed symptom from an expected result;
- reproduce a defect with the smallest useful input and read a stack trace;
- draw control flow and data flow, then write competing hypotheses and discriminating checks;
- identify a root cause instead of treating a nearby symptom;
- make the smallest safe fix and add a regression plus neighboring tests;
- inspect AI-generated diffs for hallucinated APIs, missed edges, broad exceptions, and unnecessary abstractions.

## Vocabulary preview

The [lesson](LESSON.md) defines every term before you use it:

- **Reproduction:** the smallest repeatable input and steps that trigger a bug.
- **Baseline:** behavior measured before editing.
- **Hypothesis:** a testable explanation for an observation.
- **Stack trace:** Python's record of the call path to an exception.
- **Root cause:** the condition that makes a failure possible.
- **Regression test:** a test that prevents a fixed bug from returning.
- **Diff:** the lines changed between two versions of code.

## Study order (90–150 minutes)

1. Read [LESSON.md](LESSON.md), pausing at each prediction and knowledge check (40–55 min).
2. Run [lab.ipynb](lab.ipynb) from a fresh Python 3 kernel. Predict before executing (40–60 min).
3. Finish the independent challenge and evidence handoff (10–20 min).

## Completion checklist

- [ ] I wrote observed-versus-expected behavior before changing code.
- [ ] I captured a baseline reproduction and at least three hypotheses with a check for each.
- [ ] I can explain the exact state transition that creates the duplicate.
- [ ] I tested success, invalid input, repeated keys, conflicting keys, and persistence failure.
- [ ] My regression test fails on the baseline and passes after the minimal fix.
- [ ] I reviewed every accepted diff line and verified referenced APIs instead of trusting AI prose.

## Evidence and pass conditions

Keep the baseline output, state snapshots, hypothesis log, trace/data-flow sketch, AI request and response, annotated diff, and focused/neighboring test output. The pass condition is not “the demo works”: the old reproduction must be repeatable, the new regression must prove the old code was broken, invalid and failure paths must be explicit, and no duplicate state may remain after a retry. Explain what local tests do not prove (for example, a real multi-process database race).

## Next module

Continue to [Module 15: LLM API engineering](../15-llm-api-engineering/README.md) after you can explain why evidence should precede an AI-generated patch.
