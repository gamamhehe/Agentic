---
name: Team-Standards-Instructions-Example
description: Example filled team standards file that leads can copy and adapt for a real backend repository.
---

# Example Team Standards Instructions

This example shows what a filled project-specific standards file can look like after a lead tailors it for a production API team.

## Review Mode

- Severity threshold: block `P0` and `P1`; require changes for unresolved `P2` issues on customer-facing flows.
- Architecture violations: blocking.
- Missing tests: blocking on changed Domain, Application, API contract, auth, and EF Core query behavior.
- Observability gaps: blocking on payment, identity, messaging, and job execution flows.

## Required for Feature Completion

- Happy-path test for each changed behavior path.
- Failure-path coverage for validation, auth failure, and integration failure.
- OpenAPI verification for public API contract changes.
- Structured logging for all outbound integrations and background jobs.

## Approval Required Before Implementation

- Migrations or destructive data changes.
- New vendor SDKs or HTTP integrations.
- JWT, API key, or policy changes.
- New recurring jobs.

## Forbidden Shortcuts

- Business logic in minimal API handlers.
- Direct repository or `DbContext` usage from endpoints.
- Skipping retries, timeout handling, or telemetry for new external calls.

## Team Preferences

- Prefer nested request and response records inside use cases.
- Prefer `AsNoTracking()` on read paths.
- Prefer one concern per infrastructure DI helper method.
