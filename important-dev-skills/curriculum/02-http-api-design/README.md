# Module 2: HTTP and API design

## Outcome

Design and implement a small REST API whose methods, status codes, parameters, errors, pagination, and compatibility rules are predictable to a client.

## Lab progression

1. Start with deliberately inconsistent routes for a task or exception resource.
2. Trace the request/response lifecycle, including headers and body parsing.
3. Correct method semantics, resource paths, and status codes.
4. Separate path identity, query controls, and request-body changes.
5. Add filtering and cursor or page-based pagination with explicit limits.
6. Add idempotency where replay can create duplicate work.
7. Publish an OpenAPI contract and compare it with observed behavior.
8. Make one additive change without breaking the original client test.

## Required evidence

- Contract tests covering success, validation, absence, conflict, and server failure.
- An API decision note for pagination, idempotency, and versioning.
- Generated or hand-written OpenAPI validated against the running service.
- A backward-compatibility test using the original client request.

## Pass conditions

- HTTP behavior matches the documented contract.
- Errors use one stable representation.
- Collection limits prevent unbounded responses.
- Replaying an idempotent operation does not duplicate its effect.
- The learner can distinguish transport success from business success.
