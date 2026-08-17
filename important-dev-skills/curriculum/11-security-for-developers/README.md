# Module 11: Security for developers

## Start here

Security protects assets from actors across trust boundaries. This module uses harmless strings and an in-memory SQLite database. You will reproduce and fix ownership, SQL, mass-assignment, output, path, and secret-handling mistakes without contacting a real system.

Assume Modules 1–10: HTTP inputs, SQL basics, errors, tests, and telemetry. Every new security term is defined in [LESSON.md](LESSON.md).

## Vocabulary preview

- **Asset:** something worth protecting, such as a document or token.
- **Trust boundary:** where data or authority enters more trusted code.
- **Authorization:** deciding what an authenticated actor may do.
- **Mass assignment:** allowing every submitted field to change a record.
- **Parameterized SQL:** sending values separately from SQL syntax.
- **Output escaping:** encoding text so it stays data in its context.
- **Least privilege:** granting only the access a job requires.
- **Residual risk:** harm or uncertainty that remains after a fix.

## What you will know and do

- draw assets, actors, entry points, trust boundaries, and threats;
- trace input to a dangerous sink;
- enforce server-side authorization and explicit writable fields;
- use parameterized SQL, HTML escaping, and safe path checks;
- handle secrets, dependencies, configuration, and privilege safely.

## Study order and time

Read [LESSON.md](LESSON.md), keep payloads synthetic and local, then run [lab.ipynb](lab.ipynb). Stop if an experiment would leave the fixture.

## Completion checklist

- [ ] I wrote three predictions about a trust boundary or input sink.
- [ ] I reproduced at least two harmless local flaws.
- [ ] I fixed root causes rather than filtering one string.
- [ ] I tested allowed, denied, malformed, and variant inputs.
- [ ] I found no secret in source, logs, prompts, or outputs.
- [ ] I recorded residual risk and what needs a security owner.

## Evidence and pass conditions

Keep a scope statement, threat map, harmless before/after tests, configuration/dependency/privilege review, AI diff review, and residual-risk note. You pass when authorization is deny-by-default, untrusted input cannot reach unsafe construction, secrets stay absent, reproductions remain inside the synthetic fixture, and remaining owner decisions are explicit.

## Next module

Continue to [Module 12: Docker, environments, and CI/CD](../12-docker-environments-cicd/README.md), where secure boundaries extend to builds and runtime configuration.

Previous: [Module 10: Logging, monitoring, and tracing](../10-logging-monitoring-tracing/README.md).
