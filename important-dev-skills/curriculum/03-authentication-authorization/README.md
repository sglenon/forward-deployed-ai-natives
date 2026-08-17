# Module 3: Authentication and authorization

## Start here

**Authentication** answers “who are you?” **Authorization** answers “may you do this?” They are different checks. In this local-only module you will store password *hashes* (one-way verification values), create opaque sessions, and enforce roles and ownership. The code uses `hashlib.pbkdf2_hmac` for demonstration; production systems should use a maintained password library, strong policy, secure secret storage, and a reviewed session/token design. We will not invent a production JWT signer.

You should know Python dictionaries and assertions plus Module 2 request/response boundaries. All users, tokens, clocks, and resources are synthetic.

## Vocabulary preview

- **Authentication:** checking evidence to establish who a caller is.
- **Authorization:** deciding whether that identified caller may perform an action.
- **Hash:** a one-way verification value; it is not recoverable plaintext.
- **Salt:** random per-password data stored with a hash.
- **Session:** server-side state connecting a credential to a subject and lifecycle.
- **Claim:** an assertion about a subject, such as an expiry or role, that must be validated.
- **Revocation:** marking a still-unexpired credential unusable.

The full [lesson](LESSON.md) introduces each term with synthetic examples.

## What you will know and do

- distinguish authentication, authorization, role, permission, ownership, claim, session, access credential, and refresh credential;
- hash and verify passwords with a salt and a deliberately fixed clock;
- model opaque local sessions, expiry, refresh rotation, reuse detection, and revocation;
- enforce RBAC (role-based access control) and ownership server-side, never trusting a body user ID;
- review AI auth code for plaintext passwords, fast hashes, token leakage, missing expiry, and default-allow behavior.

## Study order and time

Read [LESSON.md](LESSON.md) first (40–55 minutes), then run [lab.ipynb](lab.ipynb) (45–75 minutes) from a fresh kernel. Predict before running and do not skip the intentionally unsafe example.

## Completion checklist

- [ ] I can point to the identity proof and the permission decision separately.
- [ ] I tested missing, malformed, expired, revoked, wrong-role, and owner-mismatch credentials.
- [ ] No plaintext password, token, or sensitive claim appears in output.
- [ ] I demonstrated refresh rotation and reuse/revocation behavior.
- [ ] Changing a body `owner_id` cannot impersonate another user.
- [ ] I reviewed AI-generated auth lines against an explicit threat note.

## Evidence and pass conditions

Keep the access matrix, password-storage evidence, redacted outputs, expiry/rotation/revocation results, and AI diff review. Pass means identity comes from validated credentials; unknown roles/actions deny; passwords are not recoverable; ownership cannot be bypassed; and the tested scope—not production security—is stated honestly. A mentor can run everything with fake users.

## Next module

Continue to [Module 4: API validation and data contracts](../04-api-validation-data-contracts/README.md), where you will constrain what authenticated callers are allowed to send.
