---
name: Team-Standards-Instructions
description: Decision-ready team defaults for review strictness, testing floors, approval gates, and backend coding preferences.
---

# Team Standards Instructions

Use this file for local team operating rules that should change agent behavior inside a specific repository.

Keep generic architecture rules in the core instructions. Keep project-specific business rules in `domain-project.instructions.md`.

## Review Mode

- Severity threshold: block `P0` and `P1` issues; return `needs-changes` for unresolved `P2` risk on changed behavior.
- Architecture violations: blocking when they cross layer boundaries or introduce new long-term coupling.
- Missing tests: blocking for changed behavior in Domain, Application, WebApi, auth, configuration, persistence, and background jobs.
- Observability gaps: blocking for critical flows, integrations, auth flows, background jobs, and migration-sensitive changes.
- Style-only findings: advisory unless they hide a correctness, readability, or maintenance risk.

## Required for Feature Completion

- At least one happy-path test for each changed behavior path.
- At least one failure-path or validation-path test for risky or externally triggered behavior.
- Authorization coverage for auth, policy, permission, or tenant-boundary changes.
- Contract verification for API request, response, serialization, or versioning changes.
- Structured logging or telemetry for critical flows, integrations, and background execution.
- Cancellation token propagation for async application and infrastructure flows.

## Approval Required Before Implementation

- Database schema changes, destructive data migrations, or backfills.
- New external service integrations or SDK adoption.
- Authentication or authorization model changes.
- New background jobs, schedulers, or long-running workers.
- Breaking API contract changes or versioning changes.
- Secret-management or environment-configuration strategy changes.

## Forbidden Shortcuts

- Business logic in endpoints, middleware, filters, or controllers.
- Direct `DbContext` or infrastructure implementation usage from Application or Domain.
- Skipping tests for changed behavior because a manual check passed once.
- Swallowing exceptions without adding context, diagnostics, or intentional mapping.
- Logging secrets, tokens, raw credentials, or sensitive payloads.

## Team Preferences

- Prefer explicit request and response records over loosely shaped anonymous objects.
- Prefer one public type per file and file-scoped namespaces.
- Prefer `TypedResults`, strong OpenAPI metadata, and thin endpoint handlers.
- Prefer strongly typed options classes over scattered configuration lookups.
- Prefer structured logging with named placeholders and stable event intent.
- Prefer targeted refactors that preserve behavior and improve boundary clarity over broad rewrites.

## Pull Request Approval Expectations

- Breaking changes must include rollout notes and consumer impact.
- Migration or data-safety work must include rollback or mitigation notes.
- Auth, integration, and job changes must include observability and failure-handling evidence.
- Review approval should be withheld when the change is safe in isolation but unsafe to operate in production.
