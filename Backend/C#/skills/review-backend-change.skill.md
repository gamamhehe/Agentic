# Review Backend Change Skill

## When to use

Reviewing a local backend change, generated code, staged patch, or a focused code slice before or during implementation.

## Load this additional guidance

Assume `@Backend-Engineer` has already loaded the core backend instructions.

- `instructions/cross-cutting/21-testing.instructions.md`
- layer instructions for touched layers
- `instructions/project/team-standards.instructions.md` when local review strictness exists

## Patterns

Only patterns relevant to touched code.

## Inputs

- changed files or code slice
- intended behavior
- known risky areas
- whether the change is generated, manual, or mixed

## Steps

1. Identify the intent and the touched layers.
2. Review correctness and architecture before style.
3. Check naming, structure, validation, and error handling.
4. Check async behavior, nullability, and data access assumptions when relevant.
5. Check whether tests are missing for changed behavior.
6. Separate blocking issues from advisory cleanup.
7. Flag missing guidance when the review reveals repeated confusion.

## Output

- prioritized findings with severity
- why each finding matters
- concrete fix direction
- missing test suggestions
- guidance gaps when present

## Checklist

- [ ] Correctness is prioritized
- [ ] Architecture violations are called out
- [ ] Findings are concrete, not vague
- [ ] Test gaps are identified
- [ ] Guidance gaps are flagged when relevant
