---
name: Review-Gates-Instructions
description: Pull request protection gates for regression, security, compatibility, and operational safety.
applyTo: "**"
---

# Review Gates Instructions

Use this file for pre-merge protection checks.
Use `23-pr-review.instructions.md` for the compact review workflow and output shape.

## Blocking Gate Categories

A change is blocked from approval when one of these gates fails.

1. Correctness and regression safety
2. Architecture and boundary compliance
3. Security and authorization safety
4. Data and migration safety
5. Contract compatibility and rollout safety
6. Test coverage for changed behavior
7. Operational readiness (logging, metrics, configuration)

## Required Checks

## Correctness

- New behavior has deterministic success and failure handling.
- State-changing flows handle partial failure risk.

## Architecture

- Layer dependency direction remains valid.
- No transport/persistence models leak into Domain.

## Security

- Auth and authorization changes are explicitly tested.
- Sensitive data is not logged.
- Secrets are never hardcoded.

## Data Safety

- Schema changes include migration strategy and rollback notes.
- Data backfill and idempotency are addressed when needed.

## Contract Safety

- API contract changes are documented as breaking or non-breaking.
- Versioning strategy is explicit for breaking changes.

## Testing

- At least one test covers each changed behavior path.
- Risky code paths have failure-path tests.

## Operational Readiness

- New settings are documented and validated.
- Observability is added for new critical paths.
- Timeouts, retries, and cancellation are handled for external dependencies.

## PR Verdict Model

Use one verdict:

- `blocked` -> one or more blocking gates failed
- `needs-changes` -> non-blocking but important fixes required
- `approved-with-notes` -> safe to merge with advisory follow-ups

Every blocking finding must include:

- gate category
- risk statement
- concrete remediation
