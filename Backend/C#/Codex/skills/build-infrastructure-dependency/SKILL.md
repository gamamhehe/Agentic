---
name: build-infrastructure-dependency
description: Add or update persistence, caching, external integrations, telemetry, background jobs, or configuration-backed infrastructure in a C# and .NET backend.
---

# Build Infrastructure Dependency

Assume Codex has already read the repository `AGENTS.md`.

## When to use

Use this skill when the primary change is to persistence, external integrations, caching, background jobs, configuration-backed dependencies, or observability infrastructure.

## Primary boundary

Technical/platform boundary.

## Out of scope

- business rule design
- endpoint contract design
- project bootstrap or general repository setup

## Typical inputs

- dependency or technical concern to implement
- persistence or external service details
- configuration needs
- resiliency or observability needs

## Workflow

1. Confirm the implementation belongs in infrastructure rather than domain or transport.
2. Define or reuse the application-facing abstraction if one is needed.
3. Implement the dependency in the correct technical boundary.
4. Treat configuration and request tracking or observability as subcases of this skill, not separate skills.
5. Add logging, retries, timeout handling, and failure mapping intentionally.
6. Flag approval gates before new integrations, schema work, or jobs.
7. Recommend integration tests or focused unit tests.

## Output

- implemented dependency summary
- interface and DI changes
- config or observability changes
- risk notes and test recommendations

## Escalate to / pair with

- pair with `build-use-case` when application orchestration must consume the new dependency
- pair with `write-tests` for integration or failure-path coverage
