# Update Domain Model Skill

## When to use

Changing entities, value objects, enums, aggregates, or domain rules.

## Load this additional guidance

Assume `@Backend-Engineer` has already loaded the core backend instructions.

- `instructions/layers/10-domain.instructions.md`
- `instructions/project/domain-project.instructions.md` when project domain rules exist
- `instructions/project/team-standards.instructions.md` when approval or modeling rules exist
- `instructions/cross-cutting/21-testing.instructions.md` when tests are in scope

## Patterns

- `patterns/domain.pattern.md`
- `patterns/entity-framework-core.pattern.md` only when persistence impact matters

## Inputs

- business concept
- required properties
- invariants or rules
- relationships to other domain types
- persistence impact if known

## Steps

1. Confirm the change belongs in Domain, not Application, Infrastructure, or WebApi.
2. Update the domain type and make rules explicit.
3. Keep framework, transport, and persistence concerns out of Domain.
4. Validate how the change affects relationships and invariants.
5. Note downstream impact on UseCases, persistence, and API contracts.
6. Suggest unit tests for invariants and behavior.

## Output

- domain change summary
- invariants or business rules affected
- downstream impact notes
- test recommendations

## Checklist

- [ ] Domain remains framework-agnostic
- [ ] No DTOs or EF Core mappings leak into Domain
- [ ] Business rules are explicit
- [ ] Project-specific domain rules are respected
