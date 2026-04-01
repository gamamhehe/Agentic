---
name: Team-Standards-Instructions-Template
description: Recommended starting template for repository-specific review gates, testing floors, approval rules, and team preferences.
---

# Team Standards Instructions

Copy this file to `team-standards.instructions.md` for a new project, then replace the example defaults with real team decisions.

Keep this file focused on repository-specific operating rules. Do not repeat architecture, naming, or framework guidance that already exists elsewhere.

## How to customize this file

- Keep the structure stable so Copilot can find the same decision categories in every repository.
- Replace only the parts your team wants to tighten or relax.
- Prefer explicit thresholds over blanks, placeholders, or "use judgment" language.

## Review Mode

- Severity threshold: block `P0` and `P1`; require changes for unresolved `P2` risk on changed behavior.
- Architecture violations: blocking when they break the dependency direction or move business logic into the wrong layer.
- Missing tests: blocking for changed behavior, auth, config, persistence, and contract changes.
- Observability gaps: blocking for critical paths, jobs, and integrations.
- Style-only findings: advisory.

## Required for Feature Completion

- Happy-path coverage for each changed behavior path.
- Failure-path or validation-path coverage for externally triggered behavior.
- Authorization coverage for auth and policy changes.
- Contract verification for request, response, serialization, and versioning changes.
- Logging or telemetry for critical flows and external integrations.
- Cancellation token propagation in async application and infrastructure code.

## Approval Required Before Implementation

- Schema changes, data migrations, or backfills.
- New external services or SDKs.
- Auth model changes.
- New jobs, schedulers, or workers.
- Breaking API contracts.
- Secret-management changes.

## Forbidden Shortcuts

- Business logic in endpoints or middleware.
- Direct infrastructure access from Domain or Application.
- Skipping tests for changed behavior.
- Logging secrets or sensitive payloads.

## Team Preferences

- Prefer explicit request and response records.
- Prefer typed results and complete OpenAPI metadata.
- Prefer strongly typed options classes.
- Prefer structured logging.
- Prefer narrow refactors that preserve behavior.

## Pull Request Approval Expectations

- Breaking changes include rollout notes.
- Migration work includes rollback notes.
- Integration and job changes include observability and failure-handling evidence.
