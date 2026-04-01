---
name: build-infrastructure-dependency
description: Add or update persistence, caching, file storage, external APIs, telemetry, or background job infrastructure in a C# and .NET backend.
---

# Build Infrastructure Dependency

## When to use

Use this skill when adding or updating persistence, caching, file storage, external API integration, telemetry, or background job infrastructure.

## Load this guidance

- `instructions/layers/12-infrastructure.instructions.md`
- `instructions/layers/11-application.instructions.md` when interfaces or application contracts change
- `instructions/cross-cutting/20-configuration.instructions.md` when config changes are needed
- `instructions/cross-cutting/21-testing.instructions.md`
- `instructions/project/team-standards.instructions.md` when approval gates or platform rules exist

## Use these patterns as examples

- `patterns/infrastructure.pattern.md`
- `patterns/entity-framework-core.pattern.md` for EF Core work
- `patterns/hangfire.pattern.md` for background jobs
- `patterns/configuration.pattern.md` for options and binding

## Inputs

- dependency or technical concern to implement
- persistence or external service details
- configuration needs
- resiliency or observability needs

## Workflow

1. Confirm the implementation belongs in Infrastructure.
2. Define or reuse the Application abstraction that Infrastructure will implement.
3. Implement the dependency in the correct Infrastructure location.
4. Register it through the right DI concern in `DependencyInjection.cs`.
5. Add strongly typed configuration when required.
6. Add logging, telemetry, retries, timeout handling, or error mapping intentionally.
7. Stop for approval before new external integrations, database schema work, or background jobs if the task is not already approved.
8. Recommend integration tests or focused unit tests.

## Output

- implemented dependency summary
- interface and DI changes
- config changes
- risk notes and test recommendations
