# Refactor Backend Feature Skill

## When to use

Improving structure, readability, cohesion, or boundaries without changing intended behavior.

## Load this additional guidance

Assume `@Backend-Engineer` has already loaded the core backend instructions.

- layer instructions for touched layers
- `instructions/cross-cutting/21-testing.instructions.md`
- `instructions/project/team-standards.instructions.md` when local review or refactor rules exist

## Patterns

Only patterns relevant to the code being refactored.

## Inputs

- target feature or code area
- behavior that must be preserved
- current pain points
- known risky areas

## Steps

1. Identify the pain points and the target shape.
2. Confirm which behavior must remain unchanged.
3. Move code to the correct layer when boundaries are wrong.
4. Simplify control flow, naming, and duplication.
5. Remove indirection that does not add real value.
6. Keep or add regression tests for risky areas.
7. Note any follow-up guidance gaps exposed by the refactor.

## Output

- refactor summary
- behavior-preservation notes
- boundary improvements
- regression test recommendations

## Checklist

- [ ] Intended behavior is preserved
- [ ] Readability is improved
- [ ] Layer boundaries are cleaner
- [ ] Duplication or accidental complexity is reduced
- [ ] Regression risk is covered
