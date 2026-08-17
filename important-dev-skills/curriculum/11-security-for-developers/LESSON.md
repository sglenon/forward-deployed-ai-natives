# Lesson: protect trust boundaries with small, testable rules

## Learning goals

You will identify assets and actors, trace untrusted input to a sink, reproduce bounded local flaws, and fix the root cause. All examples use synthetic strings and an in-memory SQLite database. No payload reaches a shell, network, real file, or external account.

## A security mental model

An **asset** is something worth protecting: a report, token, or owner relationship. An **actor** is a person or process requesting an action. A **threat** is a way an actor could cause unwanted disclosure, change, or disruption. A **trust boundary** is a place where data or authority crosses from less trusted to more trusted code. An **entry point** receives data; a **sink** performs a sensitive operation such as SQL, HTML rendering, file access, or command execution.

Draw: browser → API entry point → authorization rule → store sink. Ask at each arrow who can change the data and which code enforces the rule. “The UI hides the button” is not authorization; a caller can skip the UI.

## Vocabulary

- **Authentication:** proving who an actor is.
- **Authorization:** deciding what an authenticated actor may do.
- **Broken access control:** missing or incorrect authorization, such as owner A reading B's record.
- **Mass assignment:** accepting every input field and letting a caller set protected fields.
- **Parameterized SQL:** sending values separately from SQL code so input is not interpreted as SQL syntax.
- **Command injection:** untrusted text changes a command interpreted by a shell; this lesson explains it without executing a command.
- **Output encoding/escaping:** representing text safely for its output context, such as HTML.
- **Path traversal:** using path syntax to escape an intended directory.
- **CSRF:** tricking a browser carrying credentials into sending an unwanted state-changing request.
- **SSRF:** making a server request an unintended internal or external destination.
- **Least privilege:** giving an actor or process only the access required for its job.
- **Secret:** credential or private key that grants access; synthetic examples are still handled as if sensitive.

## Why filtering one payload fails

Security is about an unsafe boundary, not a famous string. Blocking one SQL keyword does not make string-built SQL safe; another encoding or operator may bypass it. Parameterization changes the interpreter boundary. Server-side ownership checks prevent a whole class of cross-user reads. Canonical path plus an allowlist checks where a path resolves. HTML escaping encodes for the context.

## Worked authorization and mass assignment

```python
def get_document(doc, actor_id):
    if doc["owner_id"] != actor_id:
        return {"status": 404}  # avoid revealing protected existence
    return {"status": 200, "doc": doc}

WRITABLE = {"title", "body"}
def update_document(doc, fields):
    for key in WRITABLE:
        if key in fields:
            doc[key] = fields[key]
    return doc
```

The server checks ownership even if the caller supplies an ID. The update uses an allowlist so a caller cannot set `owner_id` or `role`. A `404` versus `403` choice depends on disclosure policy; document it and test it consistently.

## Parameterized SQLite

Unsafe construction looks like `"SELECT ... WHERE owner = '" + owner + "'"`. In SQLite, use `SELECT ... WHERE owner = ?` and pass `(owner,)` as a separate value. The database then treats the value as data. The notebook uses a harmless marker string and asserts that a second owner cannot read the first.

## Dangerous interpreters, safely explained

Never pass untrusted text to a shell. Even a benign-looking filename can contain syntax that changes execution. Prefer an API that accepts an argument list, a fixed operation, and an allowlist; in this notebook we only classify strings and assert that a safe builder rejects shell metacharacters. Similarly, an HTML template must escape `<` and `&`; a URL fetcher must allow only approved destinations and block private networks according to a real security policy.

For path handling, resolve a candidate beneath a fixed synthetic root and verify its common path is still that root. The lesson does not read or write files. For CSRF, explain same-site cookies and an anti-CSRF token; do not send a browser request.

## Secrets and configuration

A secret can leak through source, notebook output, logs, image layers, prompts, or error responses. Use placeholders such as `TEST_ONLY_NOT_A_SECRET`, pass values at runtime, redact output, and rotate a real value if it was ever exposed. Least privilege also applies to database roles, CI tokens, filesystem permissions, and dependencies. Pin and review dependencies; a scanner is evidence, not a substitute for ownership.

## Threat modeling before code

For each issue write: asset, actor, entry point, sink, precondition, impact, secure behavior, and residual risk. Ask an AI tool to propose variants, but do not paste secrets or accept a generated exploit that leaves the fixture. Verify the code and version yourself.

## AI-generated security diff review

Check authorization order and tenant scope, escaping context, canonicalization, exception disclosure, parameter binding, configuration defaults, dependency versions, and new permissions. Reject a filter that blocks one known string, a broad “admin” bypass, a secret in a test, or an abstraction you cannot explain. Keep a local-only scope statement in the evidence handoff.

## Syntax used in the notebook

`sqlite3.connect(':memory:')` creates a disposable database. `?` in SQL and a tuple of values bind input safely. `html.escape(text, quote=True)` encodes HTML metacharacters. `os.path.abspath`, `os.path.join`, and `os.path.commonpath` compare a candidate with an allowlisted root without reading a file. A set is an allowlist of writable fields.

## Common mistakes

1. Enforcing authorization only in a UI instead of at the server boundary.
2. Filtering one famous payload rather than changing the interpreter boundary.
3. Escaping for HTML while placing the same value in a URL, shell, or SQL context.
4. Accepting every update field and allowing protected owner/role changes.
5. Printing a synthetic-looking secret in a log or prompt and forgetting artifacts persist.

## Knowledge checks — pause before answers

1. Why is hiding an edit button not authorization?
2. What changes when SQL values are parameterized?
3. Why must output be encoded for its context?
4. Name two places a secret can leak besides source code.
5. What does least privilege reduce?

### Answers

1. An actor can call the endpoint directly; the server must enforce the permission.
2. The database receives the value as data rather than parsing it as SQL syntax.
3. HTML, URLs, and shell-like contexts have different interpreters; the correct encoding prevents text from becoming code in that context.
4. Logs, notebook output, prompts, image layers, error responses, CI artifacts, and shell history are examples.
5. It limits damage when an account, process, or dependency is compromised.

## Notebook preparation

Open [lab.ipynb](lab.ipynb) with a fresh kernel. All exploit markers are synthetic and local. Predict the result before each check, attempt the guided safe fix, and keep the threat map, before/after assertions, and residual-risk note.

## Summary and next connection

Security improvements come from enforcing trust boundaries, using safe interpreter APIs, limiting authority, and testing variants. In Module 12 these principles continue into Docker images, CI permissions, configuration, and release artifacts.
