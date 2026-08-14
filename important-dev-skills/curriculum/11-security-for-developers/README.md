# Module 11: Security for developers

## Outcome

Exploit common application vulnerabilities in a local synthetic environment, fix their root causes, and verify the fixes with negative tests.

## Lab progression

Use an intentionally vulnerable service containing a bounded selection of:

- broken access control and mass assignment;
- SQL or command injection;
- unsafe HTML output;
- CSRF or SSRF;
- path traversal;
- secret leakage and insecure defaults;
- vulnerable dependencies or excessive privileges.

For each selected issue:

1. State the precondition and potential consequence.
2. Reproduce it locally without real credentials, data, or external targets.
3. Trace untrusted input to the dangerous operation.
4. Fix the boundary or design flaw.
5. Add a regression test and check for related variants.

## Required evidence

- A threat and trust-boundary diagram.
- Reproduction commands using only the supplied local environment.
- Before-and-after tests for each vulnerability.
- A secret and privilege review covering code, configuration, logs, and CI.

## Pass conditions

- The fix addresses the unsafe pattern rather than one payload string.
- Access control is server-side and denies by default.
- Untrusted input never reaches interpreters through string construction.
- Secrets are absent from code, test artifacts, logs, and client responses.
- Residual risk and required security-owner decisions are explicit.
