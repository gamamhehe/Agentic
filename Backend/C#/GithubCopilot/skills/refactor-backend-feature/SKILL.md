---
name: refactor-backend-feature
description: Refactor a C# and .NET backend feature without changing intended behavior.
---

# Refactor Backend Feature

## When to use

Use this skill when the primary goal is to improve structure, readability, cohesion, or boundaries without changing intended behavior.

## Primary boundary

Lifecycle boundary: behavior-preserving structural change.

## Out of scope

- intentional business behavior changes
- new feature implementation from scratch
- broad PR approval decisions

## Typical inputs

- target feature or code area
- behavior that must be preserved
- current pain points
- known risky areas

## Workflow

1. Identify the pain points and the target shape.
2. State the invariants and externally visible behavior that must remain unchanged.
3. Move code to the correct boundary when layers are mixed.
4. Simplify control flow, naming, and duplication.
5. Keep, add, or update regression tests for risky areas.
6. Flag approval gates before touching auth, contracts, data shape, integrations, or jobs.

## Output

- refactor summary
- behavior-preservation notes
- boundary improvements
- regression test recommendations

## Escalate to / pair with

- pair with `write-tests` for regression safety
- pair with the relevant implementation skill when refactor uncovers missing feature work
