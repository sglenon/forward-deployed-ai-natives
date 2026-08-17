# Lesson: make HTTP an understandable contract

## Learning goals

After this chapter you can trace a request from a client to a router and service, choose a resource path and method, produce a stable response/error, bound a collection, and compare behavior with a local contract.

## Why this matters

An API is a boundary between programs. A human can adapt when a label moves; a program may fail because one field disappeared or a status changed. HTTP gives common vocabulary, but it does not choose your business meaning. Your code must make that meaning explicit.

## Start with the message

An **HTTP request** asks a server to act. An **HTTP response** reports what happened. In the notebook, dictionaries stand in for messages:

```python
request = {"method": "GET", "path": "/tasks/7",
           "query": {"limit": "10"}, "headers": {}, "body": None}
response = {"status": 200, "headers": {"Content-Type": "application/json"},
            "body": {"id": 7, "title": "Read"}}
```

The **method** describes intent. `GET` reads and should not change state. `POST` creates or performs an operation and is not automatically safe to replay. `PUT` replaces a known resource and is intended to be idempotent: applying the same request twice has the same intended effect. `PATCH` changes part of a resource, and `DELETE` removes or deactivates one. “Idempotent” is a promise about effect, not a promise that every response has the same status.

The **path** identifies a resource: `/tasks` is a collection and `/tasks/7` is one task. A **query parameter** modifies a read, for example `/tasks?owner=ana&limit=10`; it is not a new resource. A **header** carries metadata such as `Accept` or an idempotency key. A **body** carries structured input. Keeping these positions distinct helps clients and documentation.

## Status, headers, and content

A **status code** is a three-digit result. `2xx` says the exchange succeeded; `4xx` says the request cannot be accepted as sent; `5xx` says the service failed while handling a valid-looking request. Useful choices include `200 OK` for a successful read, `201 Created` for creation, `204 No Content` for a successful empty response, `400 Bad Request` for malformed input, `404 Not Found` for an absent resource, `409 Conflict` for a state collision, and `500 Internal Server Error` for an unexpected defect.

The status does not replace the body. A stable error envelope lets a client act without parsing prose:

```python
{"status": 400,
 "body": {"error": {"code": "invalid_limit", "message": "limit must be 1..50"}}}
```

The `Content-Type` header tells the receiver how to interpret the body. In this local model the body is already a dictionary, but the contract still says it represents JSON.

## Router and service boundary

A **router** chooses a handler based on method and path. A **service** owns a business operation. Let the router extract `task_id`, let the service return a result, and let the edge translate that result to HTTP. That separation means a missing task is not confused with a malformed URL and the service does not need to know status-code spelling.

```python
def list_tasks(tasks, owner=None, limit=20, offset=0):
    chosen = [t for t in tasks if owner is None or t["owner"] == owner]
    chosen.sort(key=lambda t: t["id"])
    return chosen[offset:offset + min(limit, 50)]
```

An unbounded list can consume memory and make response time unpredictable. A **bound** is a maximum enforced by the server, not a recommendation in a document. Offset pagination (`offset` plus `limit`) is simple but can shift when rows change. A continuation cursor can be more stable; whichever rule you choose, document ordering and maximum page size.

## Filtering, compatibility, and OpenAPI

Filtering belongs in the query when it narrows a collection. Whitelist field names and sort directions; never paste arbitrary query text into a database or evaluator. **Compatibility** means existing clients continue to understand the contract. Removing a field, changing its type, changing `200` to an unexpected error, or renaming an error code can break a client. Additive fields are often safer, but clients that reject unknown keys still need testing. A version path or media type can mark an intentional incompatible contract change.

**OpenAPI** is a machine-readable description of paths, inputs, and responses. The notebook represents a tiny OpenAPI-like dictionary locally. Treat it as a hypothesis until tests compare it to observed behavior; documentation that no test exercises drifts.

## Idempotency without overclaiming

An **idempotency key** is a caller-provided identifier for one intended operation. A server can remember `(key, request fingerprint, result)` and return the original result on a replay. A different request using the same key should be a `409` conflict. This protects the lab's in-memory create operation from a client retry; it does not solve every crash window or provide distributed exactly-once behavior.

## Syntax used in the notebook

Dictionary access (`request["method"]`) requires a key; `.get("owner")` returns a default. A list comprehension creates a list from a loop. `sorted(items, key=...)` returns a new deterministic order. `assert condition` stops with an error when an expectation is false. A function can return a tuple such as `(status, body)`, which unpacking assigns to two names.

## Common mistakes

1. Returning `200` for a business failure because the server technically replied.
2. Putting a filter in `/tasks/ana` and making it impossible to address a task whose identifier is `ana`.
3. Returning all rows despite a documented `limit`; bounds must be enforced in code.
4. Sorting by an unstable field or omitting a tie-breaker, making pages change between calls.
5. Retrying every `POST` without an idempotency strategy.
6. Exposing an exception string, SQL, or dependency URL in a client error.

## Reviewing AI-generated API code

Ask: What is the resource? Does the method match its side effect? Are path/query/body locations explicit? Are statuses and errors stable? Is collection size bounded before slicing? Is ordering deterministic? Does an idempotency key bind to the request body? Does the diff add a framework or network call the lab does not need? Compare each generated claim with a local assertion and reject speculative versioning or catch-all error handling.

## Knowledge checks — pause before answers

1. Why is `/tasks?owner=ana` usually a better collection filter than `/tasks/ana`?
2. What does `409` communicate that `400` may not?
3. Why is a server-enforced page bound necessary even when clients send `limit`?
4. What two values should be checked when an idempotency key is replayed?
5. Name one additive response change that can still break a strict client.

### Answers

1. The query narrows the task collection; the path `/tasks/ana` would normally identify one task and makes resource identity ambiguous.
2. `409` says the request shape may be valid but conflicts with current state, such as the same key representing different content.
3. A caller can omit or exaggerate `limit`. Only server enforcement protects memory and latency.
4. The key and a fingerprint of the request's meaningful content. The same key with different content must not receive the old result silently.
5. Adding a field can break a client that rejects unknown fields, so compatibility must be tested rather than assumed.

## Notebook preparation

Open [lab.ipynb](lab.ipynb), restart its kernel, and keep a contract table with method, path, inputs, status, body, bound, and error code. Predict before executing each marked cell. The notebook uses only dictionaries, lists, and a deterministic fake store.

## Summary and next connection

HTTP is a public boundary: method, resource location, parameters, headers, status, content type, and body all carry meaning. A tiny router/service split makes those meanings testable. Bounds, ordering, stable errors, compatibility tests, and explicit replay handling turn “it returns something” into a contract. Next, authentication will add a second boundary question: which caller is allowed to invoke it?

## A slower walkthrough: follow one request

Imagine a client asks `GET /tasks?owner=ana&limit=2`. The client chooses the method because it is reading, the path because it wants the task collection, and the query because owner and limit narrow that collection. The router matches `GET /tasks`; it does not perform the filtering itself. The service parses the limit, rejects an invalid value, selects Ana's records, sorts by an explicit key, and slices to the server's maximum. The response adds a status, JSON content type, and a body whose shape the client can rely on.

Now imagine `POST /tasks` creates a task. The body carries the new title and owner; an `Idempotency-Key` header identifies a replayable intent. A missing title is a 400 caller error. A valid new task is 201. The same key and same content can return the saved result; the same key with different content conflicts. This sequence gives each request part one job and makes a review concrete.

## Compatibility as a conversation

Write an old client before you edit the response: perhaps it reads `body[\"items\"]` and uses each item's `id`. An additive `limit` field is harmless to that client, but removing `items`, changing IDs from integers to strings, or changing an error code is not. Some clients reject unknown fields, so even additions need an explicit compatibility decision. A local contract dictionary is useful only when assertions compare it with observed responses.
