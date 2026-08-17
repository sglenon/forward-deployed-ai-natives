# Lesson: prove identity, then decide permission

## Learning goals

You will distinguish authentication from authorization, verify passwords without storing them, model short-lived opaque sessions, enforce role and ownership checks, and reason about expiry, refresh, rotation, and revocation.

## Two questions, two checks

**Authentication** (authn) establishes an identity from evidence such as a password or session credential. **Authorization** (authz) decides whether that established identity may perform an action on a resource. A login that succeeds does not mean the user may edit every task. Treating these as one check creates accidental access.

A **role** is a named group such as `admin` or `member`. A **permission** is a specific allowed action such as `task:read`. **Ownership** is a relationship between the authenticated subject and a resource. RBAC (role-based access control) maps roles to permissions; an ownership check adds a resource-specific condition.

## Passwords: verify, do not recover

Never store a plaintext password. A **hash** is a one-way computation used for comparison, not decryption. A **salt** is random per-password data stored beside the hash so equal passwords do not produce equal stored values. A **slow password KDF** makes guessing expensive. The notebook uses standard-library `hashlib.pbkdf2_hmac` with a fixed demonstration iteration count and random salt:

```python
import hashlib, hmac, secrets
salt = secrets.token_bytes(16)
stored = hashlib.pbkdf2_hmac("sha256", password.encode(), salt, 120_000)
ok = hmac.compare_digest(stored, candidate_hash)
```

The fixed count makes a local lesson predictable, not a production recommendation. Production should use a maintained password-hashing library and current policy, rate limits, breach handling, secure secret storage, and constant-time comparison. Hashing is not encryption: there is no key that reverses it.

## Credentials and claims

A **credential** is evidence presented on a request. An opaque token is a random identifier whose meaning lives in server-side session storage. It avoids teaching a homemade signed-token format. A **claim** is an assertion about a subject, such as subject ID, role, audience, or expiry. Claims must be validated; a request body saying `{"user_id": "admin"}` is not a credential.

An **access credential** is short-lived and used on ordinary requests. A **refresh credential** lasts longer and is exchanged for a new access credential. A **session** is server-side state connecting a credential to a subject, expiry, role snapshot or current policy, and a revocation state. Never print raw credentials in logs or responses.

## Fixed time makes expiry testable

Time is a dependency. The notebook supplies `now`, so “expires at 12:05” can be tested without waiting. A credential is valid only when it exists, has the expected type, has not been revoked, and `now < expires_at`. Decide whether role changes are checked against current user data or a snapshot; document the choice.

## Authorization at the resource boundary

The safe order is: authenticate the credential, load the resource, check permission, then check ownership/tenant. Do not decide ownership from a body field. If Alice sends `owner_id=Bob` while editing Alice's task, the server should use the authenticated subject and stored task owner, not the submitted owner. Unknown roles and actions should deny by default.

```python
def can_edit(session, task):
    if "task:edit:any" in session["permissions"]:
        return True
    return "task:edit:own" in session["permissions"] and task["owner_id"] == session["subject"]
```

The function answers one policy question. A handler still returns a safe `401` for absent/invalid credentials and `403` for an authenticated subject without permission (or uses a deliberate anti-enumeration policy).

## Refresh rotation and revocation

**Rotation** invalidates a refresh credential when exchanged and issues a new one. Reuse of the old credential is suspicious; the lab revokes the session family and denies it. **Revocation** marks a credential/session unusable before natural expiry, for example on logout or suspected theft. Write down the scope: one access token, one refresh token, or the whole family. Expiry limits exposure but does not undo a credential already used.

## Common mistakes

1. Using a fast hash such as raw SHA-256 for passwords.
2. Comparing hashes with ordinary `==` when a constant-time comparison is available.
3. Trusting role or user ID supplied in JSON.
4. Returning a valid-looking token in a debug response or log.
5. Treating “logged in” as permission to access another owner's row.
6. Refreshing the same token forever without rotation or reuse detection.

## Reviewing AI-generated auth code

Check the password algorithm and salt handling against maintained documentation; ask where the iteration policy comes from. Check expiry with a controllable clock, credential storage and revocation, rotation/reuse behavior, default-deny policy, ownership query, and output/log redaction. Reject invented JWT signing, secrets in source, broad exception catches, and claims of “secure” unsupported by tests. A security review should inspect every line that creates, parses, or logs a credential.

## Knowledge checks — pause before answers

1. Which question does authentication answer, and which does authorization answer?
2. Why is a unique salt needed for each password?
3. Why cannot a request body's `owner_id` establish identity?
4. What should happen when a rotated refresh credential is reused?
5. What does an access-token expiry limit, and what does it not undo?

### Answers

1. Authentication proves who the caller is; authorization decides what that subject may do.
2. It prevents equal passwords from producing equal stored values and defeats reuse of precomputed tables.
3. The caller controls the body. Identity must come from validated credential evidence and the resource's stored ownership.
4. Deny it and, in a documented policy, revoke the refresh family because reuse may indicate theft.
5. It limits how long an unused credential remains accepted; it cannot undo an action performed while the credential was valid.

## Notebook preparation

Use a fresh kernel and synthetic users only. Keep an access matrix (role × action × ownership), a redacted result log, and the exact fixed times used for expiry. The notebook's password KDF is educational; do not copy its iteration count or storage format into a production system without review.

## Summary and next connection

Authentication creates a trustworthy subject; authorization combines permissions with resource facts. Salted slow hashes protect stored password verification values. Opaque, expiring sessions reduce token-format mistakes, while rotation and revocation define lifecycle. Next, validation will constrain the input before an authorized operation mutates state.

## A slower walkthrough: from login to an edit

Imagine Alice types a password into a login form. The server looks up Alice's password record, which contains a salt and KDF output. It runs the same KDF on the candidate password and compares the two outputs. If they differ, the server must not create a session. If they match, it creates random opaque access and refresh identifiers in server-side storage. Notice the sequence: the password proves identity; the session is the later credential. A task body is not involved in either decision.

Alice then sends an access credential while editing task 7. The server first checks that the credential exists, is the right kind of credential, is not revoked, and has not expired. It obtains `subject = alice` from session state. It loads task 7 and checks the action against Alice's role and the stored `owner_id`. Only after those checks does it validate an allowed edit and save. If a caller changes `owner_id` in the JSON, that field is ignored or rejected because the caller is not the source of authority.

### A lifecycle table

| Moment | State | Decision |
| --- | --- | --- |
| Before login | no session | deny protected request |
| Password matches | new access + refresh | allow authentication response |
| Access before expiry | active | authenticate, then authorize |
| Access at/after expiry | expired | deny; client may use refresh |
| Refresh exchange | old refresh consumed | issue replacement pair |
| Old refresh reused | suspicious/revoked | deny and record the event |
| Logout/revocation | session marked unusable | deny even before expiry |

There are design choices the notebook intentionally makes visible. Its fixed clock makes boundary tests exact. Its opaque tokens avoid teaching a hand-rolled signed-token format. Its refresh store detects reuse, but it does not model TLS, browser cookie flags, device management, rate limiting, or a distributed race. A useful security lesson states these limits instead of calling a toy “secure.”

## What a beginner should ask about every auth line

When you see code that creates a credential, ask where its random bytes come from and where its meaning is stored. When you see code that parses a credential, ask what expiry, revocation, audience, and type checks occur. When you see an authorization branch, ask which identity is trusted and whether an unknown role falls through to denial. When you see a log statement, ask whether it contains a password, token, reset code, or sensitive claim. These questions turn a pattern into a review habit.
