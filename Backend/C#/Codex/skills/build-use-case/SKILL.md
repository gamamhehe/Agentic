---
name: build-use-case
description: Create or update application-layer orchestration, validation flow, or command-query handling in a C# and .NET backend.
---

# Build Use Case

Assume Codex has already read the repository `AGENTS.md`.

## When to use

Use this skill when the primary change is to application orchestration: command handlers, query handlers, validation flow, or feature-local execution wiring.

## Primary boundary

Application orchestration boundary.

## Out of scope

- endpoint transport concerns
- infrastructure adapter implementation
- project-wide bootstrap or repository-wide DI conventions

## Typical inputs

- feature or user action to support
- command or query shape
- validation and authorization expectations
- dependencies the use case will call

## Workflow

1. Confirm the requested behavior belongs in application orchestration.
2. Define the input and output contract for the use case.
3. Coordinate domain behavior, validation, authorization, and dependency calls explicitly.
4. Treat feature-local execution flow wiring as part of this skill, not as a separate skill.
5. Keep infrastructure and transport details behind stable boundaries.
6. Recommend tests for orchestration, validation, and important failure paths.

## Output

- use-case summary
- orchestration or validation notes
- dependency contracts used
- recommended tests

## Escalate to / pair with

- pair with `update-domain-model` when business rules or aggregates must change
- pair with `build-infrastructure-dependency` when new adapters or integrations are required
- pair with `write-tests` for behavior coverage
