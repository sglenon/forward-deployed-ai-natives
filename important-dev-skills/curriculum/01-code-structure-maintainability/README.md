# Module 1: Code structure and maintainability

## Start here

This is the first module in the course. You will learn how to make a small program easier to change without changing what it does. The program is an in-memory task service: it creates tasks, checks who owns them, and returns simple dictionaries that stand in for API responses. Nothing contacts a server or writes to a real database.

You do not need to know classes or software architecture before starting. The lesson introduces those ideas with small examples. You should be able to run a Python file or notebook cell, assign a value to a variable, and read an `if` statement and a `for` loop. If those are new, spend a few minutes with the official Python tutorial first.

## What you will know and do

By the end, you should be able to:

- point to the different jobs mixed together in a tangled function;
- explain why a function, module, or class has a responsibility;
- describe coupling (how much pieces depend on each other) and cohesion (how well a piece's jobs belong together);
- use composition and explicit dependency injection to give a function a fake store or clock in a test;
- recognize when DRY, KISS, or YAGNI is helpful and when it is an excuse for extra abstraction;
- write characterization tests that record existing behavior before a refactor;
- review an AI-generated diff and remove code that is speculative or impossible to explain.

## Vocabulary preview

The full lesson defines each term before asking you to use it. In short:

- **Function:** a named recipe that receives inputs and returns a result.
- **Module:** one Python file that groups related names.
- **Class/object:** a class describes a kind of thing; an object is one created instance of it.
- **Responsibility:** one job a piece of code owns.
- **Coupling/cohesion:** how much code depends on another piece / how well a piece's jobs fit together.
- **Dependency injection:** passing a needed collaborator into code instead of making it secretly create one.
- **Characterization test:** a test that records what existing code currently does before you change its structure.

## Study order and time

Plan for 90–150 minutes:

1. Read [LESSON.md](LESSON.md) (35–50 minutes). Answer the knowledge checks before opening their answers.
2. Open [lab.ipynb](lab.ipynb) and run the environment check and baseline (10–15 minutes).
3. Work through the predictions, tests, and incremental refactor (35–60 minutes). Do not skip the TODO before viewing the solution.
4. Complete the independent challenge, exit questions, and evidence checklist (10–20 minutes).

You may stop between sections, but finish by restarting the kernel and running the notebook top-to-bottom.

## Completion checklist

- [ ] I can explain every unfamiliar line in the notebook's final solution.
- [ ] I wrote at least three predictions before running code and checked each explanation.
- [ ] I recorded the tangled baseline's behavior with characterization tests.
- [ ] I made a responsibility map and wrote a falsifiable pre-edit hypothesis.
- [ ] I tested a valid request, an invalid/unauthorized request, and a dependency failure.
- [ ] I passed a fake repository and fixed clock explicitly rather than using global state.
- [ ] I reviewed the intentionally over-engineered AI-style design and can name at least two unnecessary parts.
- [ ] I can show a clean fresh-kernel notebook run.

## Evidence and pass conditions, in learner language

Keep these artifacts in your notes (or in a private copy of the lab):

- baseline and final outputs for the same representative task operations;
- tests written before the refactor plus focused tests for the extracted rule;
- a responsibility map and the hypothesis you wrote before editing;
- passing positive, negative, and failure-path checks;
- any AI prompt/completion you used, a line-by-line diff review, and suggestions you rejected.

You pass when the public task results and error behavior stay the same, the core rule can be tested without HTTP or a real database, the store and clock can be replaced in tests without changing global state, and each abstraction has a current consumer and a reason. You must be able to explain what your evidence proves and what it does not prove. Do not claim concurrency, real database, or production safety from this local exercise.

The original lab's measurable evidence is still required: a mentor should be able to run the local tests, inspect the fake dependency, and reproduce unchanged public behavior without external access. A good refactor may leave a small amount of duplication when sharing it would make the code less clear.

## Next module

When you can describe the boundary between a task service and its transport, continue to [Module 2: HTTP and API design](../02-http-api-design/README.md). It will show how that boundary becomes a predictable public contract.
