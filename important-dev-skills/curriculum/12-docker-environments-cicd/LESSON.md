# Lesson: make builds and releases repeatable

## Learning goals

You will read container and pipeline definitions as data, identify mutable or unsafe inputs, and design gates for build, test, health, migration, promotion, and rollback. The notebook is deliberately safe: it never invokes Docker or a shell.

## Vocabulary

- **Image:** a packaged filesystem and metadata used to start containers.
- **Container:** a running process created from an image.
- **Dockerfile:** instructions for building an image.
- **Stage:** a named part of a multi-stage Dockerfile; build tools can stay out of the runtime stage.
- **Workdir:** the default directory inside a container.
- **Runtime user:** the OS identity running the process; non-root limits damage.
- **Compose:** a description of several local services, networks, ports, and volumes.
- **Volume:** storage mounted outside a container's writable layer.
- **Configuration:** values that change between environments, such as a host or feature flag.
- **Secret:** sensitive configuration that must not be baked into source or image layers.
- **CI (continuous integration):** automated checks on a change.
- **Artifact:** a built, identifiable output such as an image digest.
- **Readiness:** evidence that a candidate can serve its workflow.
- **Migration:** a controlled schema/data change.
- **Rollback:** returning traffic or code to a known-good version.

## Why “works on my machine” happens

Two environments differ when Python/dependency versions, OS libraries, configuration, schema, or startup order differ. A Dockerfile can make some inputs repeatable, but an unpinned base image or dependency remains mutable. A CI file can be valid YAML and still skip the only test that catches a bug. Repeatability means recording inputs and proving the same gates run before promotion.

## Read a Dockerfile as a recipe

```dockerfile
FROM python:3.12-slim AS build
WORKDIR /build
COPY requirements.lock .
RUN pip install --prefix=/out -r requirements.lock

FROM python:3.12-slim
RUN useradd --create-home app
WORKDIR /app
COPY --from=build /out /usr/local
COPY app.py .
USER app
CMD ["python", "app.py"]
```

The build stage contains installation work; the runtime copies only needed artifacts. A fixed workdir makes relative paths predictable. `USER app` avoids root. A lock file pins direct inputs, but the base image digest and transitive artifacts still need a policy. `CMD` uses an argument list rather than a shell string.

## Compose and configuration

Compose describes services such as `api` and a disposable `db`, their ports, networks, health dependencies, and volumes. Keep the host port explicit and avoid publishing a database unnecessarily. Put a synthetic password in runtime environment configuration, not the image. “Environment variable” does not automatically mean safe: it can appear in process inspection or logs, so scope and redact it.

Development, test, staging, and production often share a configuration shape but not values. A startup check should fail clearly when required configuration is missing; it should not print the value.

## CI as a sequence of gates

A useful pipeline is checkout pinned revision → formatting/lint → unit tests → integration tests → security/dependency review → build artifact → inspect → deploy candidate → readiness/smoke → promote. A failed early gate must stop later stages. Permissions and tokens should be minimal. Never run untrusted pull-request code with deployment credentials.

## Health, migrations, and rollback

Liveness says the process runs. Readiness says it can serve. A deployment should build an identifiable artifact, apply a backward-compatible migration, start a candidate, wait for readiness, run a smoke check, then shift traffic. Expand/contract migration patterns keep old and new code compatible. Rollback of code may not undo an irreversible data migration; record that limitation.

## Validate definitions without invoking tools

The notebook parses small Dockerfile/Compose/pipeline fragments as strings and checks rules: non-root user, workdir, pinned inputs, no secret-like literals, required stages, and a failing test gate before build. This validates policy, not actual image contents. Optional local terminal practice can inspect a disposable image if your environment permits; never publish it or use real secrets.

## AI-generated build diff review

Check every base image tag, action version, cache key, user, copy path, port, permission, secret reference, and health command against the local tool/version. Reject root runtime, `latest`, secret echo, broad permissions, untrusted cache poisoning, and nonexistent action options. A syntactically valid generated file is not evidence that a release is safe.

## Syntax used in the notebook

The notebook treats definitions as strings, so `in` checks whether a directive is present and a regular expression detects a secret-like assignment. A dictionary models Compose services and pipeline stages. `list.index()` lets us compare gate order. These checks validate policy; they never execute Docker or shell syntax.

## Common mistakes

1. Assuming `latest` or an unpinned action is a stable input.
2. Running the application as root or copying build tools and secrets into runtime.
3. Publishing a database port just because a local service needs it.
4. Deploying before tests, security checks, readiness, or smoke evidence.
5. Promising code rollback reverses an incompatible data migration.

## Knowledge checks — pause before answers

1. Why use a non-root runtime user?
2. What does a lock file help with, and what can it leave mutable?
3. Why should readiness gate promotion?
4. Why can a code rollback be unsafe after a schema change?
5. What must happen after a CI test gate fails?

### Answers

1. A compromised process has fewer permissions and a smaller blast radius.
2. It records dependency versions; base image digests, OS packages, and tooling may still change without a fuller pinning policy.
3. It demonstrates the candidate can serve its intended workflow, not merely that a process started.
4. Old code may not understand the new schema or data; migrations need compatibility and rollback planning.
5. Later build, deployment, and promotion stages must stop.

## Notebook preparation

Open [lab.ipynb](lab.ipynb) in a fresh kernel. Do not run Docker, subprocesses, shells, or filesystem writes. Predict validation results, attempt the guided policy function, and save the evidence handoff including its limits.

## Summary and next connection

Repeatable delivery records inputs, separates runtime configuration, runs with least privilege, and promotes only after tests and health evidence. Module 13 uses the same evidence-first habit to choose one scalability intervention from measured constraints.
