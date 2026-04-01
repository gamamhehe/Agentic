---
name: review-backend-change
description: Review a local backend change, staged patch, or focused code slice in a C# and .NET repository. Use when you need a correctness-first review before or during implementation.
---

# Review Backend Change

## When to use

Use this skill when reviewing a local backend change, generated code, staged patch, or focused code slice before or during implementation.

## Load this guidance

- `instructions/cross-cutting/21-testing.instructions.md`
- touched layer instructions
- `instructions/project/team-standards.instructions.md` when local review strictness exists

## Workflow

1. Identify the intent and the touched layers.
2. Review correctness and architecture before style.
3. Check naming, structure, validation, error handling, async behavior, nullability, and data-access assumptions when relevant.
4. Check whether tests are missing for changed behavior.
5. Separate blocking issues from advisory cleanup.
6. Flag missing guidance when the review reveals repeated confusion.

## Output

- prioritized findings with severity
- why each finding matters
- concrete fix direction
- missing test suggestions
- guidance gaps when present
