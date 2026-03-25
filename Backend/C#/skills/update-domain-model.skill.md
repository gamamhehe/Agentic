# Update Domain Model Skill

## When to use

Changing entities, value objects, enums, or domain rules.

## Instructions to load

- `instructions/core/01-architecture.instructions.md`
- `instructions/core/02-naming.instructions.md`
- `instructions/layers/10-domain.instructions.md`
- `instructions/project/*.instructions.md` — when project-specific rules exist
- `instructions/cross-cutting/21-testing.instructions.md` — when tests in scope

## Patterns

- `patterns/domain.pattern.md`
- `patterns/entity-framework-core.pattern.md` — only when persistence impact matters

## Inputs

- Business concept
- Required properties
- Invariants or rules
- Relationships to other domain types
- Persistence impact if known

## Steps

1. Confirm change belongs in Domain — not Application, Infrastructure, or WebApi
2. Update domain type and invariants
3. Keep framework and persistence concerns out
4. Validate relationships with existing entities, value objects, enums
5. Note downstream impact on handlers, EF Core config, API contracts
6. Suggest unit tests for invariants and behavior

## Checklist

- [ ] Domain remains framework-agnostic
- [ ] No DTOs or EF Core mappings in Domain
- [ ] Business rules explicit
- [ ] Project-specific rules respected
