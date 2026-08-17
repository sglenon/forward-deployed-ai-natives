# Debugging a seeded bug and reviewing an AI fix

## What you will learn

By the end you can turn a vague report into a reproducible experiment, follow values through unfamiliar code, choose between competing explanations, and review a small patch. You will practice on a save-note operation where a retry creates a duplicate note.

## Why debugging is a skill

Software rarely announces its cause. A user says “I clicked once and got two notes,” but that sentence contains a symptom, not an explanation. **Debugging** is the disciplined process of comparing observed behavior with expected behavior, gathering evidence, and changing the responsible code. An **incident** is an unexpected event that matters to users or operators. The safe debugger reduces uncertainty one check at a time.

An AI assistant can summarize code quickly, but it can also invent a method, fix a nearby line, or hide an edge case behind a large rewrite. You remain responsible for behavior. A test that fails on the old code and passes on the new code is more useful than a confident paragraph.

## Vocabulary

- **Symptom:** what you can observe, such as a count of two notes.
- **Expected behavior:** the result the product rule says should happen.
- **Reproduction:** the smallest repeatable input and steps that trigger a bug.
- **Baseline:** behavior measured before editing.
- **Stack trace:** Python's record of the call path and line where an exception was raised.
- **Control flow:** the order in which statements and branches run.
- **Data flow:** how a value changes as it moves through functions.
- **Hypothesis:** a testable explanation, not a guess treated as fact.
- **Discriminating check:** a small observation that supports one hypothesis and rules out another.
- **Root cause:** the condition that makes the failure possible.
- **Regression test:** a test that prevents a fixed bug from returning.
- **Diff:** the added, removed, and changed lines between two versions.
- **Idempotency:** repeating the same operation has the same effect as doing it once.
- **Idempotency key:** a client-provided identifier used to recognize a retry.

## A mental model: observation → evidence → change

Use this loop:

```text
report → exact reproduction → baseline trace/state → hypotheses
      → discriminating checks → smallest fix → regression + neighbors
```

Do not skip directly from report to “fix.” A report says what a caller saw. A trace records the path and values. A hypothesis predicts an observation. A fix changes code only after one hypothesis survives its checks.

For the note service, the invariant is simple: one idempotency key represents one logical save. If the first request succeeds and the client retries, the second request should return the original note or a safe duplicate response, but storage must contain one note.

## Read the smallest Python program

The notebook uses dictionaries and functions. A dictionary maps names to values:

```python
request = {"text": "Reset password", "key": "k-1"}
request["text"]                 # required key; raises KeyError if missing
request.get("owner", "unknown") # optional key with a default
```

`def` creates a function and `return` sends a result to its caller. A list is an ordered mutable collection; `notes.append(note)` adds a record. `assert condition, "message"` stops with an `AssertionError` when an expectation is false. A `try`/`except` block can observe an expected exception, but catching every exception usually hides programming errors.

An exception is Python's way of reporting that normal execution cannot continue. Its stack trace starts at the failing line and shows who called it. Read from the bottom line for the exception type/message, then walk upward to understand the route that delivered the bad value.

## Reproduce before inspecting a proposed solution

Write a reproduction as inputs, actions, observations, and expected result:

```text
input: text='Reset password', owner='sam', key='k-1'
actions: save once, then repeat the identical request
observed: two records in notes
expected: one record; retry is idempotent
```

Make the fixture deterministic: clear the list, use known strings, and print state after each call. A reproduction that depends on “sometimes” is a starting point; reduce it until it is reliable. The notebook deliberately makes the bug occur every time.

## Follow control flow and data flow

A typical save function has these jobs:

1. validate text and owner;
2. look up the retry key;
3. create a note object;
4. append it to storage;
5. remember the key and return a response.

The bug is an ordering error: the baseline appends before checking whether the key was already seen. Draw the actual order, not the order you wish existed:

```text
request → validate → build note → append note → check key → return
                                  ^ duplicate already exists here
```

A **state transition** is a change from one observable state to another. The dangerous transition is `one note + known key` to `two notes + known key` on the retry. The validation function may look suspicious because it is nearby, but if inputs are already valid it cannot explain a duplicate.

## Hypotheses and discriminating checks

Good hypotheses are specific and falsifiable:

| Hypothesis | Smallest check | Result that weakens it |
| --- | --- | --- |
| retry key is ignored | print keys before/after two identical calls | key is present and equal |
| validation runs twice | use a valid request and count validation calls | validation is called once per request |
| fixture was not reset | clear storage and print initial length | initial length is zero |
| write happens before deduplication | trace storage length at each line | length grows before key check |

The best check is cheap and isolates one uncertainty. “Run everything again” may confirm a failure but does not discriminate between causes.

Record hypotheses before editing. If a check surprises you, update the log rather than changing the code to fit the first story.

## Root cause versus symptom

“The count is two” is the symptom. “The operation mutates storage before it decides whether this key was already processed” is a root-cause statement because it identifies the enabling condition. “The validation function is confusing” is not a root cause unless a validation result can cause the duplicate.

Use a causal chain:

```text
same key arrives
 → baseline builds a new note
 → baseline appends without checking existing keys
 → key lookup happens too late
 → retry creates a second visible record
```

A minimal fix moves the decision to the write boundary and returns the previously stored note for a matching key. A different payload using an existing key must be rejected as a conflict; silently returning unrelated data is unsafe.

## Tests that prove the fix

First write a characterization test or executable reproduction that captures the old behavior. Then add a regression test with a name that describes the invariant. Test neighboring risks too:

- valid first save creates one record;
- identical retry does not add a record;
- same key with different text is a conflict;
- missing text/owner is rejected before storage;
- a new key creates a second record;
- a simulated persistence failure leaves no half-written state.

**Positive testing** checks a valid operation. **Negative testing** checks invalid input or denied behavior. **Failure-path testing** checks an unavailable dependency or exception. A green test suite is evidence about cases you wrote, not proof of every concurrent database behavior.

## A bounded patch

The smallest safe change is local:

```python
if key in seen:
    old = by_key[key]
    if old["text"] != text:
        return {"status": 409, "error": "key already used"}
    return {"status": 200, "note": old}
note = {"id": len(notes) + 1, "key": key, "text": text}
notes.append(note)
by_key[key] = note
return {"status": 201, "note": note}
```

The real service would need an atomic database uniqueness constraint for concurrent writers. This notebook's in-memory dictionary proves ordering and behavior, not multi-process safety.

## Reviewing AI-generated code

Give an AI tool a verified report, relevant snippets, failing output, and constraints. Ask for two hypotheses and a bounded patch plan before code. Never paste secrets or real incident data.

Review the response in four passes:

1. **API reality:** does every function, argument, package, and option exist in the checked-out version? Search the repository or official local docs.
2. **Behavior:** does the diff enforce the invariant at the responsible boundary? Run the old reproduction and edge cases.
3. **Scope:** did it alter unrelated validation, status codes, logging, schema, or configuration? Remove speculative abstractions.
4. **Tests:** can each new test fail on the old code? Watch for tests that only assert the new implementation or mock away the bug.

Common AI mistakes include `dict.setdefault` used with a side effect that still writes, broad `except Exception` that hides malformed input, an imagined `is_retryable()` method, and a lock that protects only one process. Ask the AI to attack its own patch, but reproduce useful findings yourself.

## Common mistakes

- Editing before capturing baseline state, so you cannot prove the fix.
- Calling a hypothesis “the root cause” without a discriminating check.
- Reading a stack trace only for the final line and ignoring the call path.
- Returning success for a conflicting key because “the retry worked.”
- Adding retries around a non-idempotent write without an idempotency boundary.
- Treating a large refactor as a debugging fix.
- Logging full user text or keys when a redacted ID would be enough.

## Knowledge checks — answer before opening the answers

1. Why is “two rows” a symptom rather than a root cause?
2. What makes a check discriminating?
3. Which invariant should the retry regression test assert?
4. Why is a local dictionary not proof of concurrent database safety?
5. Name two things to verify in an AI-generated diff before running it.

### Answers

1. It describes an observation but not the condition that made it possible. The ordering of write and key check is a causal explanation.
2. It is designed so different hypotheses predict different outcomes.
3. Repeating one valid key leaves one stored note and returns the original result; a conflicting payload is rejected.
4. Two processes can interleave between a check and write; a real store needs an atomic uniqueness constraint or transaction.
5. Verify referenced APIs exist and inspect behavior/scope; also require tests that fail on the baseline.

## Notebook preparation

Open [lab.ipynb](lab.ipynb) with Python 3.10+. Restart the kernel, run all cells in order, and keep your predictions in a notes file. The notebook writes no files and imports only `traceback`, `time`, and other standard-library modules. Every check is deterministic.

## Summary and next connection

Debugging is evidence-driven: reproduce, trace, hypothesize, discriminate, patch narrowly, and test neighbors. AI can accelerate searching and generate alternatives, but it cannot replace a regression test or your explanation of the diff. In Module 15 you will apply the same boundary discipline to unreliable model providers, where malformed output and retry cost become new failure modes.
