# Module 12: Docker, environments, and CI/CD

## Start here

Packaging is a promise that the same inputs produce a runnable artifact. You will study Dockerfiles, Compose-like service descriptions, and CI pipelines as data—without invoking Docker, a shell, a network, or writing secrets to disk.

Assume Modules 1–11: configuration, tests, security, health, and release failure concepts. Optional terminal practice is not required for the notebook.

## Vocabulary preview

- **Image:** packaged filesystem and metadata used to start containers.
- **Container:** a running process created from an image.
- **Stage:** a part of a multi-stage build with its own files/tools.
- **Runtime user:** the OS identity running the process.
- **Compose service/volume:** a described component / mounted storage.
- **CI gate:** an automated check that can stop a later stage.
- **Artifact:** an identifiable build output.
- **Readiness/rollback:** evidence a candidate can serve / returning to a known-good release.

## What you will know and do

- distinguish images, containers, stages, users, ports, volumes, and services;
- separate runtime configuration and secrets from source and image layers;
- validate Compose and CI definitions as structured text;
- design pinned inputs and gates for tests, health, migration, promotion, and rollback.

## Study order and time

Read [LESSON.md](LESSON.md), then run [lab.ipynb](lab.ipynb) from a fresh kernel. The notebook never calls Docker, `subprocess`, or a shell.

## Completion checklist

- [ ] I wrote three predictions about a build or release risk.
- [ ] I can explain why a non-root runtime and pinned input matter.
- [ ] I validated a Dockerfile, service fragment, and CI stage list.
- [ ] I kept synthetic secrets out of artifacts and logs.
- [ ] I showed a failing gate before build/promotion.
- [ ] I wrote a readiness, migration, and rollback limitation.

## Evidence and pass conditions

Keep validation results, expected runtime user/files/ports, configuration and secret policy, failing/passing gate transcripts, release order, rollback note, and AI diff review. You pass when local/CI inputs match, runtime is appropriately minimal/non-root, gates stop bad candidates, secrets stay out of artifacts/logs, and data compatibility limits are explicit.

## Next module

Continue to [Module 13: Scalability and production system design](../13-scalability-system-design/README.md), where measurements choose the next bounded change.

Previous: [Module 11: Security for developers](../11-security-for-developers/README.md).
