# Module 12: Docker, environments, and CI/CD

## Outcome

Package an API and its dependencies into a repeatable environment, then build an automated path from pull request checks to a reversible deployment.

## Lab progression

1. Containerize the API with a small, non-root runtime image.
2. Run the API, PostgreSQL, and Redis or queue dependency through Compose.
3. Separate configuration from code and distinguish development, test, staging, and production values.
4. Keep secrets out of images, repository history, and logged environment dumps.
5. Add CI stages for formatting or linting, tests, security checks, and image build.
6. Pin or record dependency and image versions sufficiently for repeatability.
7. Add a deployment gate, health verification, and rollback procedure.
8. Rehearse a failed release and rollback in a disposable environment.

## Required evidence

- A clean build from a fresh checkout.
- CI output for both a failing and passing change.
- Image inspection showing the expected user, files, and configuration behavior.
- Timestamped deployment and rollback drill notes.

## Pass conditions

- Local and CI commands produce the same test result.
- Runtime images contain no development secrets or unnecessary build tools.
- Migrations have an explicit place in the release sequence.
- Health verification can block or reverse a bad release.
- Rollback limitations, including database compatibility, are documented.
