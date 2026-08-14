# Module 8: Testing production code

## Outcome

Take an AI-generated feature and determine whether it works by writing tests designed to expose its assumptions and failure paths.

## Lab progression

1. Translate the feature claim into observable acceptance conditions.
2. Add a small unit test around deterministic domain logic.
3. Add an integration test across the real application boundary and a disposable database.
4. Add an end-to-end test for one critical user flow.
5. Write regression tests for a seeded defect.
6. Test boundary values, malformed input, dependency failure, concurrency, and authorization denial.
7. Replace mocks that merely restate implementation with fakes or real boundaries where confidence requires them.
8. Inspect coverage as a navigation aid, not a quality score.

## Required evidence

- A test map showing which risk each level covers.
- At least one test that reveals a false assumption in the generated feature.
- A regression test that fails before the fix and passes after it.
- A list of important behavior intentionally not mocked.

## Pass conditions

- Tests assert behavior rather than private implementation structure.
- Failure paths receive deliberate coverage.
- The suite is deterministic and isolated enough for CI.
- Database tests use a realistic schema and lifecycle.
- The learner can state what the passing suite still does not prove.
