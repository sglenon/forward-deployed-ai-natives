# Lesson: tests that teach you whether a feature works

## Learning goals

After this chapter you can describe a feature as observable conditions, choose a test boundary, build isolated fixtures, and interpret a green suite without overclaiming. You will use only `assert` and plain Python functions in the notebook.

## Why testing matters

A **test** is a small program that asks a question about other code. A passing test is evidence for that question, not proof that every possible input works. An AI-generated test may look professional while repeating the implementation: it can call the same helper, mock the database that contains the bug, or assert only that a function returned something. Good tests start with the user-visible contract.

Our example lists reports belonging to an owner. A contract says: owner A can see A's reports, not B's; page size is bounded; malformed input is rejected; and a storage outage is visible as an error. These are conditions a user or caller can observe.

## Vocabulary

- **Assertion:** a check that raises an error when an expectation is false (`assert 2 + 2 == 4`).
- **Unit test:** checks one small unit with collaborators replaced or absent.
- **Integration test:** checks that real pieces work together at a boundary, such as Python code with SQLite.
- **End-to-end (E2E) test:** follows a user journey through the outermost available interface.
- **Regression test:** a test added to prevent a bug from returning.
- **Fixture:** known setup data and cleanup used by a test.
- **Isolation:** one test cannot change what a later test sees.
- **Mock:** a programmable double that records calls and can return values.
- **Stub:** a double that supplies canned answers.
- **Fake:** a lightweight working implementation, such as an in-memory store.
- **Coverage:** which lines or branches ran; it does not measure whether assertions were meaningful.

## A mental model: arrange, act, assert

Most tests have three parts. **Arrange** creates inputs and collaborators. **Act** calls the behavior under test. **Assert** checks an observable result or side effect.

```python
# arrange
reports = [{"id": 1, "owner": "ana", "title": "Plan"}]
# act
result = list_reports(reports, "ana", limit=10)
# assert
assert result["items"] == reports
```

Keep the reason for each assertion visible. If a test checks `result["items"]`, it can catch a changed ownership filter. If it checks only that `list_reports` was called, it cannot.

## Test levels and choosing a boundary

A unit test is cheap and precise. Use it for pure pagination or validation rules. An integration test costs more but catches wiring, schema, SQL, and serialization errors. Use a real disposable SQLite database when the risk is a SQL query or ownership predicate. An E2E test is valuable for one critical journey but can be slower and harder to diagnose. A regression test is about purpose, not a fourth technical level: it can be a unit or integration test.

Do not choose a level because a pyramid diagram says so. Ask: where could the defect occur, and what is the cheapest boundary that would observe it? If you replace SQLite with a mock, you cannot prove the SQL query filters owners.

## Isolation and realistic SQLite

The notebook creates a fresh SQLite connection per test. SQLite is a small relational database available in Python's standard library. A transaction groups changes; rolling it back or deleting the in-memory database prevents data leaking between tests. A fixture should be deterministic: same seed, same schema, same expected rows.

An in-memory fake is useful for a unit test of service logic. SQLite is useful for the integration boundary. Neither proves a production database's indexes, network behavior, or permissions. Record that limit.

## Doubles: mock, stub, fake

Suppose a service sends a notification after a report is created. A stub can return “sent” without contacting anything. A mock can record that the notification was called once. A fake notification sink can store messages in a list. Use the least clever double that makes the boundary safe. Mocking the database in a database query test removes the risk you meant to test.

## Worked example: an unsafe baseline

```python
def list_reports(rows, owner, limit=20, cursor=0):
    # An AI-style mistake: paginate before filtering ownership.
    page = rows[cursor:cursor + limit]
    visible = [row for row in page if row["owner"] == owner]
    return {"items": visible, "next": cursor + limit if len(page) == limit else None}
```

If the first page contains only another owner's rows, the caller gets an empty page and may stop even though their report is on the next slice. The implementation also accepts negative limits unless a boundary validates them. Write the test from the contract first. Do not copy the slice expression into the expected result.

## Boundaries worth testing

Positive cases include one owner's report, multiple pages, and an empty result. Negative cases include a missing owner, limit zero, a limit above the maximum, malformed cursor, and an unknown report. Authorization cases prove that a second owner cannot read the first owner's record. Failure cases make a fake store raise a controlled exception and verify the service returns a documented error rather than pretending success.

Boundary tests are not random extremes. A boundary is where behavior changes: zero versus one, maximum versus maximum plus one, owner A versus owner B, available versus unavailable dependency.

## Coverage is not confidence

Line coverage answers “did execution visit this line?” Branch coverage asks whether true and false paths ran. Neither asks whether the expected value was correct. A test that executes a broken function and asserts `True` creates coverage without confidence. Use coverage as a map to find unvisited risk, then read assertions and contracts.

## Reviewing AI-generated tests

Ask an AI tool for a test plan, then verify every case against the real contract. In a diff review ask: would this test fail if ownership were removed? Does it use a fresh fixture? Does the mock hide SQL? Does the test assert status, shape, ordering, and data—not just a call count? Are APIs and imports real? Delete speculative helpers and tests that mirror private implementation.

## Syntax used in the notebook

`def test_name():` defines a plain test function; calling it runs the question. `assert actual == expected` stops on a false expectation. `try`/`except` observes a controlled dependency error. `sqlite3.connect(':memory:')` creates a disposable database, `execute(sql, (value,))` binds a parameter, and a list comprehension creates filtered data.

## Common mistakes

1. Sharing one mutable fixture between tests and letting order decide the result.
2. Mocking the database in the test whose purpose is to verify SQL ownership filtering.
3. Asserting only status or a call count while ignoring returned data.
4. Writing an expected result by copying the production algorithm.
5. Treating coverage or one happy path as proof of authorization and failure behavior.

## Knowledge checks — pause before answers

1. Why is a SQLite test an integration test while an in-memory list test can be a unit test?
2. What defect can a test that asserts only `status == 200` miss?
3. When is a fake preferable to a mock?
4. Why does coverage not prove correctness?
5. What makes a fixture isolated?

### Answers

1. SQLite exercises a real collaboration between application code, SQL, schema, and database behavior. A list test can isolate one function without that boundary.
2. It can miss wrong owners, missing fields, wrong ordering, empty-page cursors, or leaked error details.
3. Use a fake when a small working implementation makes the behavior realistic and easy to inspect; use a mock when interaction itself is the contract, such as “send once.”
4. Coverage measures execution, not whether assertions would fail for a defect.
5. It starts with known data and leaves no shared mutable state that changes another test's result.

## Notebook preparation

Open [lab.ipynb](lab.ipynb), restart the kernel, and run every cell in order. Before each prediction, write your answer in a note. The TODO cell is intentionally executable starter code; attempt a test before reading its reference solution. Save the test map and evidence handoff.

## Summary and next connection

Tests are executable questions about contracts. Arrange–act–assert keeps those questions readable; fixtures keep them repeatable; unit and integration boundaries reveal different risks. Use doubles deliberately, include negative and failure paths, and treat coverage as navigation. In Module 9 you will test a stateful queue, where recovery and duplicate delivery make the observable contract even more important.
