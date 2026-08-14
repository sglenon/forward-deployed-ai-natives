# Module 4: API validation and data contracts

## Outcome

Turn an API that accepts arbitrary JSON into one with explicit request, response, and error contracts.

## Lab progression

1. Reproduce mass assignment, wrong types, missing fields, unknown fields, unsafe nesting, and invalid enum values.
2. Gate supported content types and body sizes.
3. Add a schema for each write operation rather than one universal model.
4. Reject unknown input and map allowed fields explicitly.
5. Separate input, domain, and response models.
6. Normalize validation failures into the API error contract.
7. Add contract tests for optional, nullable, and omitted values.

Use the project’s standard schema tool, such as Pydantic, Zod, JSON Schema, or an equivalent. The concepts matter more than the library.

## Required evidence

- A payload corpus containing valid, boundary, malformed, and malicious examples.
- Tests that show the unsafe baseline and the final rejection behavior.
- Request and response schemas visible in the OpenAPI contract where applicable.
- A field-level error example that is useful without exposing internals.

## Pass conditions

- Invalid states are rejected before business logic runs.
- Unknown fields cannot alter protected state.
- Response serialization does not leak internal or sensitive fields.
- Errors are stable enough for a client to act on.
- The learner can explain required, optional, nullable, defaulted, and omitted values.
