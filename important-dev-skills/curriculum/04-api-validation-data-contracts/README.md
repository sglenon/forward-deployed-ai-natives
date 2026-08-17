# Module 4: API validation and data contracts

## Start here

Validation is the act of checking whether input has an allowed shape and value before business logic runs. A **data contract** is the shared promise about fields, types, omissions, and errors. You will build explicit standard-library validators for a task API: parse a request, validate an input model, map it to a domain model, and serialize a safe response. No package or network is needed.

You should know JSON-like dictionaries, lists, strings, numbers, and Module 2 API boundaries. Every example uses synthetic bounded payloads.

## Vocabulary preview

- **Parsing:** turning incoming bytes or JSON-like data into a program value.
- **Validation:** checking that a value has an allowed shape and meaning.
- **Serialization:** shaping internal data for a client response.
- **Nullable:** allowed to contain `null`.
- **Omitted:** not supplied at all; it may mean “leave unchanged.”
- **Enum:** a finite set of allowed values.
- **Mass assignment:** copying caller fields into protected internal fields.

The full [lesson](LESSON.md) works through these ideas before the notebook.

## What you will know and do

- distinguish parsing, validation, serialization, request/domain/response models;
- explain required, optional, nullable, omitted, defaulted, enum, nested, and unknown fields;
- reject wrong types, unsupported media, oversized/deep payloads, and protected/mass-assignment fields;
- return stable field-level errors before state mutation;
- review AI schemas for silent coercion, permissive unknown fields, and accidentally exposed storage fields.

## Study order and time

Read [LESSON.md](LESSON.md), pause for the checks, then execute [lab.ipynb](lab.ipynb) in a fresh kernel. Plan 90–150 minutes and keep a payload corpus in your notes.

## Completion checklist

- [ ] I can explain `null` versus omitted for create and update.
- [ ] I tested valid, boundary, malformed, unknown, protected, oversized, and unsafe-nesting payloads.
- [ ] Invalid input is rejected before business logic or persistence.
- [ ] Input, domain, and response mappings are separate.
- [ ] Errors are stable without stack traces or internals.
- [ ] I reviewed AI coercions and schema options line by line.

## Evidence and pass conditions

Keep the payload corpus, baseline/final mutation counts, field errors, contract comparison, and AI review. Pass means invalid types, missing values, enums, media, size, structure, unknown/protected fields are consistently handled; response exposure is intentional; and all claims are local and reproducible.

## Next module

Continue to [Module 5: SQL and database schema design](../05-sql-schema-design/README.md), where validated data meets durable constraints.
