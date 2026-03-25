# Refactor Backend Feature Skill

## When to use

Improving structure, readability, or boundaries without changing intended behavior.

## Instructions to load

- `instructions/core/01-architecture.instructions.md`
- `instructions/core/02-naming.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md`
- Layer instructions for touched layers

## Patterns

Only patterns relevant to code being refactored.

## Steps

1. Identify pain points and target shape
2. Confirm behavior to preserve
3. Move code to correct layer when boundaries are wrong
4. Simplify control flow, improve naming, remove duplication
5. Remove abstractions that add indirection without value
6. Keep or add regression tests for risky areas
7. Note follow-up guidance to document

## Checklist

- [ ] Behavior preserved
- [ ] Readability improved
- [ ] Boundaries improved
- [ ] Duplication reduced
- [ ] Test coverage sufficient
