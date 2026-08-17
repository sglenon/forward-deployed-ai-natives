# Module 8: Testing production code

## Start here

Tests are small programs that check whether another program keeps its promises. In this module you build a tiny report service and choose tests that catch real mistakes. Everything is local Python: no pytest, network, or shared database is required.

You should be comfortable with functions, dictionaries, exceptions, SQL basics, and request/response boundaries from Modules 1–7. New terms are explained in [LESSON.md](LESSON.md) before the notebook uses them.

## Vocabulary preview

- **Assertion:** a check that raises an error when an expectation is false.
- **Fixture:** known setup data used by a test.
- **Unit test:** checks one small unit in isolation.
- **Integration test:** checks real pieces working together, such as code and SQLite.
- **Regression test:** prevents a fixed bug from returning.
- **Mock/stub/fake:** test doubles that record calls, return canned data, or provide a small working implementation.
- **Coverage:** code that ran; it is not proof that assertions are meaningful.

## What you will know and do

- use arrange–act–assert and isolated fixtures;
- choose unit, integration, and end-to-end boundaries;
- test happy paths, boundaries, authorization, and failures;
- detect AI-generated tests that create false confidence.

## Study order and time

Plan for 90–150 minutes: read [LESSON.md](LESSON.md), answer checks before their answers, then run [lab.ipynb](lab.ipynb) from a fresh kernel. Pause before predictions and TODOs.

## Completion checklist

- [ ] I wrote three predictions before running code.
- [ ] I used a fresh fixture for each test.
- [ ] I have a regression test for an ownership or boundary defect.
- [ ] I can explain why the SQLite test is an integration test.
- [ ] I rejected at least one false-confidence AI test.
- [ ] I can name what passing tests do not prove.

## Evidence and pass conditions

Keep a test map, baseline failure and fixed regression, positive/negative/failure outputs, fixture-isolation evidence, and an annotated AI diff review. Include authorization denial, dependency failure, boundary inputs, and a short coverage interpretation. You pass when tests check observable contracts, run repeatedly with synthetic SQLite data, and you can explain each mock and remaining blind spot.

## Next module

Continue to [Module 9: Async processing, queues, and background jobs](../09-async-queues-background-jobs/README.md). Its worker tests depend on the isolation and failure-path habits practiced here.

Previous: [Module 7: Error handling and resilience](../07-error-handling-resilience/README.md).
