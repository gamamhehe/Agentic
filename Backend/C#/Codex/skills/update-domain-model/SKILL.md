---
name: update-domain-model
description: Change entities, value objects, aggregates, invariants, or domain services in a C# and .NET backend.
---

# Update Domain Model

Assume Codex has already read the repository `AGENTS.md`.

## When to use

Use this skill when the primary change is to business concepts, invariants, entity behavior, value objects, or domain policies.

## Primary boundary

Business/domain boundary.

## Out of scope

- endpoint transport design
- infrastructure adapter implementation
- project bootstrap or configuration glue

## Typical inputs

- business rule change
- aggregate or entity to update
- invariant or validation requirement
- events or domain side effects when relevant

## Workflow

1. Confirm the change belongs in the domain model rather than in application or infrastructure.
2. Update entities, value objects, aggregates, or domain services with explicit invariants.
3. Keep persistence, transport, and framework concerns out of the domain shape.
4. Call out downstream application, endpoint, or persistence impacts.
5. Recommend tests that prove the new invariant or business behavior.

## Output

- domain change summary
- affected invariants or rules
- downstream impact notes
- recommended domain-focused tests

## Escalate to / pair with

- pair with `build-use-case` when orchestration must change around the new domain behavior
- pair with `write-tests` for invariant and rule coverage
