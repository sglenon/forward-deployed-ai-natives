# Lesson: make code easier to change

## Learning goals

After this chapter, you will be able to read a small unfamiliar program and answer three questions:

1. What jobs does this code perform?
2. Which jobs should change together, and which should be independent?
3. What is the smallest safe change that makes a job easier to test?

You will practice those questions on a tiny task service. The goal is not to create a grand architecture. The goal is to make one useful boundary visible while preserving behavior.

## Why structure matters

Imagine a sandwich shop where one person takes the order, bakes the bread, charges the card, stores ingredients, and delivers the sandwich. The shop can work, but changing the payment provider means disturbing the oven and delivery process too. In software, a large function can have the same problem: it parses input, checks rules, writes data, reads the current time, and formats a response. A **service** is a program or program component that performs a useful operation for another caller; our task service performs task operations. A **handler** is the function at the edge of a program that receives an incoming request and turns the result into a response.

That code may pass a happy-path demo. It becomes expensive when a second feature needs one of the same rules, or when a test needs to use a fake clock instead of waiting for real time. Good structure gives each job a sensible home and gives tests a way to replace slow or unpredictable collaborators.

“Maintainable” does not mean “many files” or “lots of classes.” It means a future reader can find a responsibility, predict the effect of a change, and verify it with a small test.

## Start with a motivating example

Here is a deliberately tangled function. A **function** is a named recipe: it receives values, performs steps, and usually returns a value. The `create_task` function below does at least five jobs:

```python
from datetime import date

TASKS = []

def create_task(request):
    # 1. Transport parsing: pull fields from a request-shaped dictionary.
    title = request.get("title", "").strip()
    owner = request.get("owner", "").strip()

    # 2. Input validation.
    if not title or not owner:
        return {"status": 400, "error": "title and owner are required"}

    # 3. Business rule: a title may not be longer than 80 characters.
    if len(title) > 80:
        return {"status": 400, "error": "title is too long"}

    # 4. Persistence: save data in a global list.
    task = {"id": len(TASKS) + 1, "title": title, "owner": owner,
            "created_on": date.today().isoformat()}
    TASKS.append(task)

    # 5. Response formatting.
    return {"status": 201, "task": task}
```

The observable result is a dictionary. An **observable behavior** is anything a caller can see: the returned status, fields, errors, and the task saved in `TASKS`. A refactor is safe when it changes the internal arrangement but keeps those observations the same.

The code also hides two dependencies. A **dependency** is something a piece of code needs from elsewhere. `TASKS` is hidden storage, and `date.today()` is hidden time. Hidden dependencies make tests share state or depend on the calendar.

## A small mental model: jobs and boundaries

Before editing, make a responsibility map. A **responsibility** is a job a piece of code owns, such as “validate a title” or “save a task.” Write the map in plain language:

| Job | Current location | A useful question |
| --- | --- | --- |
| read request fields | handler | What if the input is not shaped as expected? |
| apply task rules | handler | Can I test this without a request or response? |
| choose an ID and save | global list | Can a test replace storage? |
| choose today's date | global clock | Can a test use a fixed date? |
| choose status/error shape | handler | Is this a transport concern? |

The boundary is the line across which data moves. A good boundary is often a plain function that accepts ordinary values and returns an ordinary value. You do not need a framework to create one.

## Functions, modules, classes, and objects

These words are related but not interchangeable.

### Functions

A function is a reusable recipe. `def` defines it; parentheses call it:

```python
def add_tax(price, rate):
    return price * (1 + rate)

total = add_tax(100, 0.10)  # call the recipe; total is 110.0
```

Parameters (`price` and `rate`) are named inputs. `return` sends a result back. A function should have a small, explainable job. It may call another function to delegate a detail.

### Modules

A module is one Python file. When you write `import task_rules`, Python loads the names defined in `task_rules.py`. A module is a filing cabinet: it gives related functions and classes a home and lets another file use them by name. A module is not automatically a “layer”; putting a trivial function in a new file can add searching without adding clarity.

### Classes and objects

A **class** is a description for creating objects. An **object** is one concrete value made from that description. A class can group data and behavior that naturally belong together:

```python
class FixedClock:
    def __init__(self, today):
        self.today = today

    def current_date(self):
        return self.today

clock = FixedClock("2026-01-01")  # an object, one FixedClock instance
clock.current_date()               # "2026-01-01"
```

`__init__` runs when the object is created. `self` means “this particular object.” A class is useful when several operations share state or when an object represents a replaceable collaborator. A class is not required just because a program is “professional.” A plain function can be clearer.

## Separation of concerns, cohesion, and coupling

**Separation of concerns** means keeping different kinds of decisions apart. In our example, input/response formatting is a transport concern, title rules are a business concern, and saving is a storage concern. Separating them lets a change in one concern avoid surprising another.

**Cohesion** describes whether the responsibilities in one unit belong together. A `title_rules` function that only checks titles is cohesive. A `create_task` function that also sends emails, writes SQL, and formats HTTP errors has low cohesion because unrelated jobs are bundled together.

**Coupling** describes how much one unit relies on another unit's details. If a rule directly reaches into a global list and calls the real clock, it is tightly coupled to those details. If it receives a small store and clock as inputs, it is less coupled. Low coupling makes replacement and focused testing easier.

Think of cohesion as “things in one toolbox fit together” and coupling as “how many special connectors are needed between toolboxes.” Perfectly independent code is impossible; the useful question is whether the dependency is visible, small, and justified.

## Composition versus inheritance

**Composition** means building behavior by giving an object or function other objects to use: a service *has a* store and clock. **Inheritance** means defining a new class as a specialized kind of another class: a `SqlTaskStore` *is a* `TaskStore` in an inheritance hierarchy.

Composition is usually the gentler first choice because each collaborator can be replaced directly:

```python
class TaskService:
    def __init__(self, store, clock):
        self.store = store       # composition: service has a store
        self.clock = clock       # composition: service has a clock
```

Inheritance can be useful when a stable family really shares an interface and behavior, but it also couples the child to the parent's rules. Do not create `AbstractBaseTaskService`, `BaseRepository`, and three subclasses merely because an AI tool offered them. Start with a function or a tiny object, then add an abstraction when a current test or replacement needs it.

## Explicit dependency injection

**Dependency injection** means passing a dependency into a function or object instead of creating or looking it up secretly inside. “Injection” sounds grand, but this is just an argument. A **repository** is a component whose responsibility is storing and retrieving records; our in-memory repository is a tiny fake repository for practice:

```python
def create_task(title, owner, store, clock):
    # store and clock are explicit: a caller chooses their implementations.
    task = {"title": title, "owner": owner,
            "created_on": clock.current_date()}
    return store.save(task)
```

For a test, `store` can be a tiny in-memory fake and `clock` can always return one known date. This is safer than patching a global variable because the dependency is visible at the call site.

## DRY, KISS, and YAGNI without slogans

**DRY** means “Don't Repeat Yourself.” It warns against repeating one changing piece of knowledge in multiple places. If two handlers must obey exactly the same ownership rule, a shared rule function may prevent drift. DRY does not mean every similar-looking line needs a generic helper; two strings that happen to look alike may change for different reasons.

**KISS** means “Keep It Simple, [as the] simplest solution that works.” Prefer a direct function and a dictionary over a framework or five layers when the problem is small. Simple does not mean careless: validation and tests are still valuable.

**YAGNI** means “You Aren't Gonna Need It.” Do not build a future plugin system, cache, or interface until a current requirement or test needs it. Speculative flexibility is a cost: readers must understand it and bugs can hide in it.

These principles can conflict. A good decision names the current problem and the evidence. “I extracted this rule because two callers use it and a focused test needs it” is stronger than “architecture says we need a service layer.”

## Characterization tests before refactoring

A **characterization test** captures what existing code does, including behavior that may be awkward. It is a safety net for changing structure. It is not necessarily a statement that every existing behavior is ideal.

For the task function, characterize at least:

- a valid task and its returned fields;
- missing or invalid input;
- ownership or transition rejection, if the baseline has that rule;
- a storage failure and its current error behavior.

Run these tests before moving code. If a test fails before your refactor, first decide whether the failure is a bug in the baseline or an incorrect expectation. Do not silently “fix” behavior while claiming a structure-only refactor.

## Incremental refactoring walkthrough

Refactoring means changing internal design while preserving observable behavior. Make one small change, run tests, then make the next.

### Step 1: isolate the business rule

Start with a pure function. **Pure** means that, for the same inputs, it returns the same result and does not change outside state.

```python
def validate_task(title, owner):
    title = title.strip()
    owner = owner.strip()
    if not title or not owner:
        return "title and owner are required"
    if len(title) > 80:
        return "title is too long"
    return None
```

The function returns an error message or `None` (meaning no error). It does not know about HTTP status codes or the list used for storage. Test it with ordinary strings.

### Step 2: make storage and time replaceable

The core operation can now receive a store and clock:

```python
def create_task_record(title, owner, store, clock):
    error = validate_task(title, owner)
    if error:
        return {"ok": False, "error": error}
    task = {
        "id": store.next_id(),
        "title": title.strip(),
        "owner": owner.strip(),
        "created_on": clock.current_date(),
    }
    store.save(task)
    return {"ok": True, "task": task}
```

The function does not need to know whether `store` is a list-backed fake or a SQL implementation. This is a small boundary, not a promise to support every database.

### Step 3: keep transport at the edge

The handler translates request/response conventions, while the core operation speaks in task results:

```python
def handle_create(request, store, clock):
    result = create_task_record(
        request.get("title", ""), request.get("owner", ""), store, clock
    )
    if not result["ok"]:
        return {"status": 400, "error": result["error"]}
    return {"status": 201, "task": result["task"]}
```

The transport boundary is now visible. A future HTTP framework can call `handle_create`, but the rule can be tested without starting one.

## Syntax you will use in the notebook

The notebook uses only Python's standard library.

- A **dictionary** (`{"title": "Fix bug"}`) maps keys to values. Use `record["title"]` when the key must exist, or `record.get("title", "")` for a default.
- A **list** (`[]`) stores an ordered collection. `items.append(value)` adds one item.
- An assertion checks an expectation: `assert actual == expected`. If it passes, Python says nothing; if it fails, read the values in the message.
- A **dataclass** is a standard-library helper that creates a small class for data. The notebook uses ordinary dictionaries for task records, so you can focus on structure.
- `None` is Python's special value meaning “no value.” In `validate_task`, it means that no validation error was found.
- A **type hint** such as `def save(task: dict) -> None` documents an expected shape. It does not by itself validate values at runtime.
- A method call such as `store.save(task)` asks an object to perform an operation. The dot means “look up this name on that object.”
- A `try`/`except` block handles an expected exception. We use it only at the boundary where a storage failure becomes an error result; we do not hide every programming mistake.

## Common mistakes

1. **Changing behavior while moving code.** A refactor can accidentally trim a value twice, change an error status, or create IDs differently. Run characterization tests after each move.
2. **Using a global fake.** A global `TASKS` list leaks state between tests. Create a fresh fake store per test instead.
3. **Passing a giant “context” dictionary.** One dictionary containing clock, store, logger, user, settings, and future options hides dependencies. Pass only what the function uses.
4. **Confusing composition with a framework.** Passing two objects to a constructor is composition; it does not require a service container.
5. **Extracting by line count.** A short function may still contain two responsibilities; a longer cohesive function may be fine. Look at reasons for change.
6. **Trusting green tests blindly.** A test that only checks `status == 201` may miss a changed title or owner. Check meaningful observable fields.

## Reviewing AI-generated code for over-engineering

AI tools are good at producing plausible patterns. They are not responsible for the tradeoffs in your codebase. When reviewing a generated diff, ask:

- Can I explain every changed line and import?
- Does each new class/function have a current caller and one clear job?
- Did the diff preserve IDs, dates, error values, and side effects?
- Are dependencies explicit, or did the code hide them in globals or constructors?
- Did it add inheritance, a generic repository, a container, configuration, or adapters that no test uses?
- Does it catch broad exceptions and hide real programming errors?
- Are tests checking behavior rather than only implementation details?
- Did the tool invent APIs, flags, or package names that are not present locally?

An AI answer that adds six files to solve a two-function exercise may be technically polished and still be the wrong design. Ask it for the smallest change, then compare that change with your own hypothesis.

## Knowledge checks — pause before reading answers

1. In the tangled function, which two things are hidden dependencies, and why do they make tests harder?
2. What is the difference between cohesion and coupling?
3. Why can composition be a safer first choice than inheritance for a replaceable store?
4. What does a characterization test protect during a structure-only refactor?
5. Name one sign that an AI-generated abstraction is speculative.

### Answers

1. The global `TASKS` list and `date.today()` are hidden dependencies. A test cannot choose fresh storage or a fixed date without changing global state or the real calendar.
2. Cohesion asks whether the jobs inside one unit belong together. Coupling asks how much one unit depends on another unit's details. A unit can be cohesive while still tightly coupled to a global.
3. Composition passes collaborators directly, so a test can provide a fake store without inheriting parent behavior or navigating a hierarchy. Inheritance is useful for a genuine stable “is-a” relationship, but it adds a stronger relationship.
4. It records current observable behavior before editing. If the behavior changes unexpectedly, the test points to a regression even though the goal was only to change structure.
5. A class or interface has no current caller, test, or replacement need; it exists only for a predicted future feature. Extra layers that make a two-step operation harder to follow are another warning.

## Notebook preparation

Open [lab.ipynb](lab.ipynb) with your local notebook tool. Start from a fresh kernel. The notebook builds a tiny in-memory task service, so no network or file setup is required. Keep your prediction answers and responsibility map in notes. When the notebook presents a solution, compare the design reasons—not just whether your code happened to pass.

## Summary and next connection

Maintainability comes from visible responsibilities, explicit dependencies, cohesive units, and evidence that behavior stayed stable. Begin with the smallest boundary that a current test or replacement needs. Use composition and dependency injection to make unpredictable collaborators replaceable. Use DRY, KISS, and YAGNI as questions about present evidence, not as magic rules. Treat AI-generated code as a draft: inspect the diff, verify behavior, and remove abstractions you cannot justify.

In Module 2, you will apply the same boundary thinking to HTTP. You will learn which parts of a request and response are a public contract, and why changing them can break callers even when the internal code is cleaner.
