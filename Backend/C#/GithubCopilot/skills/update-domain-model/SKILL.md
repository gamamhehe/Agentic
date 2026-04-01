---
name: update-domain-model
description: Change entities, value objects, aggregates, or domain rules in a C# and .NET backend while preserving domain purity.
---

# Update Domain Model

## When to use

Use this skill when the primary change is to business concepts, invariants, aggregates, entities, enums, or value objects.

## Primary boundary

Business/domain boundary.

## Out of scope

- endpoint transport design
- application orchestration or validation flow design
- infrastructure adapter implementation
- project bootstrap work

## Typical inputs

- business concept
- required properties
- invariants or rules
- relationships to other domain types
- persistence impact if known

## Workflow

1. Confirm the change belongs in the domain boundary.
2. Make invariants and business rules explicit.
3. Keep framework, transport, and persistence concerns out of the domain model.
4. Note downstream impact on application flow, persistence, and contracts.
5. Recommend unit tests for invariants and behavior.

## Output

- domain change summary
- invariants or business rules affected
- downstream impact notes
- test recommendations

## Escalate to / pair with

- pair with `build-use-case` when domain changes require orchestration or validation updates
- pair with `write-tests` for invariant coverage
