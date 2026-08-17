# Module 2: HTTP and API design

## Start here

An **API (application programming interface)** is a set of rules that lets one program ask another program to do something. HTTP is the message format commonly used for web APIs. In this module you will model HTTP with ordinary Python dictionaries; you will not start a server or contact the internet. You will build a tiny task service and make its requests, responses, errors, and collection reads predictable.

You should be able to read Python functions, dictionaries, lists, and `assert` statements. Module 1's idea of a boundary helps: the router translates an incoming request, while a service performs the task operation.

## What you will know and do

- explain a request's method, path, query, headers, and body and a response's status, headers, and body;
- choose resource-oriented paths, method semantics, status-code classes, content types, and stable error shapes;
- implement bounded filtering, deterministic ordering, pagination, and an idempotency key in a pure-Python service;
- describe compatibility/versioning and represent a small OpenAPI contract as local data;
- review AI-generated endpoint code for unbounded reads, unsafe replays, leaked internals, and breaking response changes.

## Vocabulary preview

- **HTTP request/response:** a message sent to a server / the server's reply.
- **Resource:** a thing named by an API, such as one task or a task collection.
- **Method:** the verb describing intent, such as `GET`, `POST`, or `DELETE`.
- **Status code:** a three-digit result; 2xx means success, 4xx means caller problem, and 5xx means server problem.
- **Header/body:** metadata about a message / its content.
- **Idempotent:** repeating the same operation has the same intended effect.

## Study order and time

Plan for 90–150 minutes. Read [LESSON.md](LESSON.md), answering checks before the answers. Then run [lab.ipynb](lab.ipynb) from a fresh kernel, pausing at each prediction and TODO. Finish by restarting and running all cells top-to-bottom.

## Completion checklist

- [ ] I can label path, query, header, and body values in a request.
- [ ] I wrote three predictions and compared them with explanations.
- [ ] I bounded and deterministically ordered a collection response.
- [ ] I tested success, invalid input, missing resource, conflict, and dependency failure.
- [ ] I replayed an idempotent write and inspected its effect.
- [ ] I compared observed behavior with the local OpenAPI-shaped contract.
- [ ] I reviewed an AI-style diff and can name two rejected changes.

## Evidence and pass conditions

Keep request/response captures, a contract decision table, pre-edit hypotheses, positive/negative/failure checks, the compatibility test for the original client, and your AI prompt/diff review. You pass when paths, methods, statuses, errors, bounds, ordering, and response fields match the documented contract; repeated idempotency-key requests do not duplicate work; and claims stay limited to this local synthetic service. A mentor must be able to run it without credentials.

## Next module

Continue to [Module 3: Authentication and authorization](../03-authentication-authorization/README.md). It adds identity and permission checks at the API boundary.
