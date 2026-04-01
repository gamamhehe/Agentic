---
name: add-request-tracking
description: Add endpoint-level telemetry, request logging, and Application Insights wiring for a C# and .NET backend. Use when asked to add request tracking, correlation, telemetry, or structured logging to backend flows.
---

# Add Request Tracking

## When to use

Use this skill when adding endpoint-level telemetry, request logging, Application Insights enrichment, correlation metadata, or request-tracking middleware.

## Load this guidance

- `instructions/layers/12-infrastructure.instructions.md`
- `instructions/layers/13-webapi.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md` when tests or verification are in scope
- `instructions/project/team-standards.instructions.md` when repository observability rules exist

## Use these patterns as examples

- `patterns/logging.pattern.md`
- `patterns/api.pattern.md`

## Inputs

- endpoint or feature name
- telemetry goals
- whether request or response bodies need to be captured
- sensitive-data constraints

## Workflow

1. Confirm what decision or diagnosis the telemetry should support.
2. Keep implementation in Infrastructure and pipeline wiring in WebApi.
3. Register Application Insights and request-tracking services through Infrastructure DI.
4. Add middleware, filters, or endpoint metadata only where tracking is required.
5. Capture the minimum useful telemetry and avoid large payload logging by default.
6. Protect secrets, tokens, credentials, and sensitive payloads.
7. Recommend tests or verification steps for middleware order, redaction, and telemetry behavior.

## Output

- summary of what was tracked
- files or layers affected
- sensitive-data decisions
- tests or verification steps
