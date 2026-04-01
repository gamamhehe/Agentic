---
name: build-infrastructure-dependency
description: Add or update persistence, integrations, jobs, configuration, or observability in a C# and .NET backend.
---

# Build Infrastructure Dependency

## When to use

Use this skill when the primary change is technical/platform work such as persistence, external integrations, background jobs, configuration, telemetry, or observability.

## Primary boundary

Technical/platform boundary.

## Out of scope

- business rule design
- endpoint contract design
- pure application orchestration work
- project-wide bootstrap/setup framing

## Typical inputs

- dependency or technical concern to implement
- persistence or external service details
- configuration needs
- resiliency or observability needs

## Workflow

1. Confirm the implementation belongs in infrastructure or platform concerns.
2. Define or reuse the application-facing abstraction if one is needed.
3. Treat configuration and observability as subcases of this technical boundary, not separate top-level skills.
4. Add configuration, logging, retries, timeout handling, and failure mapping intentionally.
5. Flag approval gates before new integrations, schema work, or jobs.
6. Recommend integration tests or focused unit tests.

## Output

- implemented dependency summary
- interface and DI changes
- config or observability changes
- risk notes and test recommendations

## Escalate to / pair with

- pair with `build-use-case` when orchestration or validation must call the new dependency
- pair with `write-tests` for technical verification
