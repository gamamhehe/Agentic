---
name: update-domain-model
description: Change entities, value objects, enums, aggregates, or domain rules in a C# and .NET backend while preserving domain purity.
---

# Update Domain Model

## When to use

Use this skill when changing entities, value objects, enums, aggregates, or domain rules.

## Load this guidance

- `instructions/layers/10-domain.instructions.md`
- `instructions/project/domain-project.instructions.md` when project domain rules exist
- `instructions/project/team-standards.instructions.md` when approval or modeling rules exist
- `instructions/cross-cutting/21-testing.instructions.md` when tests are in scope

## Use these patterns as examples

- `patterns/domain.pattern.md`
- `patterns/entity-framework-core.pattern.md` only when persistence impact matters

## Inputs

- business concept
- required properties
- invariants or rules
- relationships to other domain types
- persistence impact if known

## Workflow

1. Confirm the change belongs in Domain, not Application, Infrastructure, or WebApi.
2. Update the domain type and make rules explicit.
3. Keep framework, transport, and persistence concerns out of Domain.
4. Validate how the change affects relationships and invariants.
5. Note downstream impact on use cases, persistence, and API contracts.
6. Recommend unit tests for invariants and behavior.

## Output

- domain change summary
- invariants or business rules affected
- downstream impact notes
- test recommendations
