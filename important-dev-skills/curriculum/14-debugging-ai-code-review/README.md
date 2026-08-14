# Module 14: Debugging and AI-generated code review

## Outcome

Reproduce a realistic bug, find its root cause in unfamiliar code, review an AI-proposed fix, and prove the failure is gone without introducing a regression.

## Lab progression

1. Convert a vague bug report into exact observed and expected behavior.
2. Reproduce the problem before asking an AI tool for a fix.
3. Trace the data and control flow across the relevant boundary.
4. Form competing hypotheses and run the smallest discriminating checks.
5. Give the AI tool only verified, relevant context and request a bounded proposal.
6. Review its cited APIs, assumptions, edge cases, abstractions, and full diff.
7. Reject or revise the proposal until it addresses the root cause.
8. Add a regression test and run proportionate neighboring checks.

## Required evidence

- Reproduction steps and a failing test.
- A short hypothesis log showing eliminated explanations.
- The AI request, response, and annotated diff review.
- Verification proving the root cause is removed and named behavior remains intact.

## Pass conditions

- The fix is not accepted solely because tests generated with it pass.
- Referenced functions, packages, and configuration options exist in the actual project version.
- The change is bounded to the demonstrated cause.
- Missing edge cases and unnecessary abstractions are called out.
- The learner can explain every accepted line.
