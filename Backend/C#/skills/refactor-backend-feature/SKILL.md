---
name: refactor-backend-feature
description: Refactor a C# and .NET backend feature without changing intended behavior. Use when the goal is better structure, readability, cohesion, or boundaries rather than new functionality.
---

# Refactor Backend Feature

## When to use

Use this skill when improving structure, readability, cohesion, or boundaries without changing intended behavior.

## Load this guidance

- touched layer instructions
- `instructions/cross-cutting/21-testing.instructions.md`
- `instructions/project/team-standards.instructions.md` when local review or refactor rules exist

## Use these patterns as examples

Only the patterns relevant to the code being refactored.

## Inputs

- target feature or code area
- behavior that must be preserved
- current pain points
- known risky areas

## Workflow

1. Identify the pain points and the target shape.
2. State the invariants and externally visible behavior that must remain unchanged.
3. Move code to the correct layer when boundaries are wrong.
4. Simplify control flow, naming, and duplication.
5. Remove indirection that does not add value.
6. Keep, add, or update regression tests for risky areas before declaring the refactor safe.
7. Flag approval gates before touching auth, contracts, data shape, integrations, or jobs.
8. Note any follow-up guidance gaps exposed by the refactor.

## Output

- refactor summary
- behavior-preservation notes
- boundary improvements
- regression test recommendations
