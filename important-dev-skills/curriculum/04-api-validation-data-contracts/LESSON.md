# Lesson: make input shapes explicit

## Learning goals

You will parse a request, validate a small schema without hidden coercion, map it to domain data, serialize a safe response, and explain omission, `null`, unknown fields, and protected fields.

## Why validation is a boundary

User input is data, not a promise. **Parsing** turns bytes or a JSON-like value into a programming value. **Validation** checks that value against allowed structure and rules. **Serialization** turns internal data into a response shape. Keeping these steps explicit means invalid input is rejected before business logic, persistence, or side effects.

## Four models, not one giant dictionary

An input/request model describes what the caller may send. A domain model describes what the business operation needs after validation. A storage model may contain IDs and internal columns. A response model describes what a client may see. Reusing one permissive dictionary for all four invites mass assignment: **mass assignment** is accidentally copying caller-controlled keys into protected fields such as `owner_id`, `status`, or `created_at`.

```python
def to_domain(payload, subject):
    return {"title": payload["title"].strip(),
            "priority": payload.get("priority", "normal"),
            "owner_id": subject}       # never payload["owner_id"]
```

The explicit allow-list is longer than `record.update(payload)`, but it makes authority visible.

## Required, optional, nullable, and omitted

**Required** means the key must exist. **Optional** means it may be omitted. **Nullable** means `None`/JSON `null` is an allowed value. Omitted and null are not automatically the same. For an update, omitted may mean “leave unchanged,” while null may mean “clear this field.” A default is a server choice applied when a key is absent; document it. Use a sentinel when you must distinguish omission from an explicit `None`:

```python
MISSING = object()
note = payload.get("note", MISSING)
if note is MISSING:
    pass
elif note is None:
    ...
```

## Types, enums, nesting, and bounds

A **type** says what kind of value is allowed: string, integer, boolean, list, or object. Be careful: in Python `bool` is a subclass of `int`, so a strict integer validator should reject booleans. An **enum** is a finite allowed set, such as `{"low", "normal", "high"}`. Nested objects need their own validator. Bounds (maximum body bytes, string length, list count, and nesting depth) protect memory and reasoning. Content type says whether the body is supported; a JSON endpoint should reject unsupported media before parsing as JSON.

Unknown fields deserve a policy. Rejecting them catches typos and prevents silent future behavior. Ignoring them can support forward compatibility but is dangerous when a typo changes a security-sensitive field. Choose explicitly and test it.

## Stable errors and ordering

Return a stable envelope with a machine-readable code and field path:

```python
{"error": {"code": "invalid_field",
           "fields": [{"path": "priority", "code": "not_allowed"}]}}
```

Do not return Python tracebacks, storage SQL, or raw exception text. Validate cheap shape/type rules before domain rules and before mutation. If several fields are invalid, choose deterministic ordering so tests and clients can rely on it.

## Common mistakes

1. Coercing `"12"` to `12` without documenting it, hiding client bugs.
2. Treating `null` and omission as the same update instruction.
3. Accepting arbitrary nested keys and allowing protected-field changes.
4. Validating after saving, leaving partial state on failure.
5. Checking only top-level type and allowing unbounded nested lists.
6. Returning a storage row as the response, exposing internal IDs or secrets.

## Reviewing AI-generated validators

Ask what happens for booleans-as-integers, `NaN`, unknown keys, deeply nested objects, oversized strings, omitted/null values, and duplicate list entries. Inspect coercion defaults and whether validators run before side effects. Confirm the library's actual behavior with a tiny local test rather than trusting a generated option name. Ensure response serialization is an allow-list and errors have stable codes/paths.

## Knowledge checks — pause before answers

1. Why should create and update models usually differ?
2. How can `null` and omission mean different things?
3. What is mass assignment and which field should never come from a task-create body?
4. Why can silently ignored unknown keys hide a bug?
5. Where must validation happen relative to persistence?

### Answers

1. Create often requires fields and lets the server generate values; update often makes fields optional and needs a clear “leave vs clear” rule.
2. Omission can mean “no instruction,” while null can mean “explicitly clear,” if the contract permits clearing.
3. It is copying caller-controlled input into fields the caller should not control; `owner_id`, `status`, and `created_at` are common examples.
4. A misspelled key can be silently discarded, making a caller believe a setting was applied. Security-sensitive extra keys can also signal an attack.
5. Before business logic that mutates state and before any database or external side effect.

## Notebook preparation

Prepare a payload corpus with valid, boundary, malformed, unknown, protected, wrong-content-type, oversized, and deeply nested cases. Run [lab.ipynb](lab.ipynb) from a fresh kernel and compare the mutation counter before and after each invalid request.

## Summary and next connection

Contracts become useful when parsing, validation, domain mapping, and serialization are separate and explicit. Required/optional/nullable/omitted meanings, strict types, bounds, unknown-field policy, and safe errors are all part of the contract. Next, SQL constraints provide a second line of defense after API validation.

## A slower walkthrough: create versus update

Suppose a client sends `{\"title\": \"Plan\"}` to create a task. The parser first confirms that the body is an object and that the content type is supported. The validator sees a required string and supplies the documented default priority. The domain mapper adds `owner_id` from the authenticated subject, not from the body. The storage layer may add an ID and creation time. Finally, the response mapper chooses public fields. Each arrow removes ambiguity.

Now consider an update body. An empty object can mean “change nothing,” so it should not be treated like a create request missing its title. If the body contains no `note` key, leave the old note. If it contains `\"note\": null`, clear the note if the contract allows clearing. If it contains `\"note\": 3`, reject it before touching storage. A sentinel such as `MISSING = object()` is useful because `None` is a real value and cannot also mean “not supplied.”

### Shape, value, and business checks

Validation often has layers. Shape validation asks whether the body is an object and whether required keys exist. Type validation asks whether `priority` is an integer rather than a string or boolean. Value validation asks whether the integer is between 1 and 3. Domain validation asks whether changing the task is allowed in its current state. These checks can all produce errors, but the client benefits when their paths and codes are deterministic. Keep the boundary check before any side effect.

### Bounds are part of correctness

A payload limit is not only a denial-of-service defense. It also makes a function's behavior understandable. A maximum title length, tag count, body size, and nesting depth gives reviewers a finite set of cases to reason about. A list validator should validate each item rather than checking only that the outer value is a list. A recursive depth check should stop before recursion becomes unbounded. The notebook uses small limits so you can see every rejection.

## A review exercise in plain language

Imagine an AI suggests `record.update(payload)` because it is concise. Ask which keys the caller can now set. If the record has `owner_id`, `status`, `created_at`, or an internal score, the answer is “all of them.” An allow-list projection may look repetitive, but repetition is useful when it marks an authority boundary. Also ask whether an AI schema silently converts `\"2\"` to `2`; coercion can hide a broken client and change security decisions. Write a tiny assertion for behavior you depend on rather than trusting a parameter name from generated code.
