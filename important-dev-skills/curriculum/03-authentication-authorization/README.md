# Module 3: Authentication and authorization

## Outcome

Progress from an anonymous API to one that enforces trusted identity, roles, permissions, resource ownership, token expiry, and revocation.

## Lab progression

```text
Anonymous access
→ authenticated identity
→ role and permission checks
→ resource ownership
→ short-lived access and refresh
→ rotation and revocation
```

At each stage, first demonstrate the remaining unauthorized action. Treat authentication and authorization as separate decisions.

## Required evidence

- Passwords stored with an appropriate password-hashing function rather than encryption or a fast hash.
- Negative tests for missing, invalid, expired, revoked, and stale credentials.
- An access matrix covering roles, actions, resource ownership, and tenant boundaries.
- Tests proving request-body identity cannot impersonate another user.
- A short threat note for token theft, role changes, and logout behavior.

## Pass conditions

- Authorization is enforced server-side at the resource boundary.
- Denial is the default for unrecognized roles or actions.
- Refresh use rotates or otherwise protects reusable credentials.
- Revocation behavior matches the documented promise.
- Responses and logs do not expose passwords, tokens, or sensitive claims.
