# Module 1: Code structure and maintainability

## Outcome

Refactor a working but tangled API without changing its behavior, then explain why the new boundaries are easier to test and change.

## Lab progression

1. Run the baseline and capture representative requests, responses, and tests.
2. Mark HTTP, business-rule, persistence, and configuration responsibilities in the code.
3. Extract small functions and remove duplicated behavior.
4. Separate transport, domain, and storage concerns.
5. Introduce dependencies explicitly where tests or replacement require it.
6. Review the result for speculative interfaces, wrappers, inheritance, and other AI-generated over-engineering.

## Required evidence

- Characterization tests written before refactoring.
- A responsibility map for the baseline and final structure.
- A diff showing behavior-preserving steps rather than a rewrite.
- One example where DRY helps and one where duplication is clearer than a premature abstraction.

## Pass conditions

- Public behavior remains unchanged.
- Business rules can be tested without starting the HTTP server.
- Persistence can be replaced in a test without global mutation.
- The learner can justify each abstraction with a current requirement.
- No new framework is introduced merely to organize a small program.
