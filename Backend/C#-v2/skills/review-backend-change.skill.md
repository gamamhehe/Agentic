# Review Backend Change Skill

> Cross‑project note: replace placeholders like `{Entity}` and `{ProjectName}` with real names.

## When to use

Use this skill when reviewing a backend change, pull request, or generated code.

Typical cases:
- review a new feature
- review a refactor
- review AI-generated code
- review architecture compliance
- review testing adequacy

## Relevant instructions

Load the instructions for the layers touched by the change.
Almost always include:
- `instructions/core/01-architecture.instructions.md`
- `instructions/core/02-naming.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md`

Then add the relevant layer instructions:
- `instructions/layers/10-domain.instructions.md`
- `instructions/layers/11-application.instructions.md`
- `instructions/layers/12-infrastructure.instructions.md`
- `instructions/layers/13-webapi.instructions.md`
- `instructions/cross-cutting/20-configuration.instructions.md`

## Related patterns

Use only the patterns relevant to the touched code.

## Steps

1. Identify the impacted layers and main intent of the change
2. Review architecture boundaries first
3. Review correctness and behavior risks
4. Review naming and structure consistency
5. Review validation, authorization, and error handling
6. Review observability and operational concerns when relevant
7. Review test coverage and missing cases
8. Separate critical issues from optional improvements

## Output

- prioritized review findings
- explanation of why each issue matters
- concrete fixes or guidance
- suggested missing tests
- suggested guidance updates when needed

## Checklist

- architecture boundary violations are called out
- correctness issues are prioritized
- review is concrete, not vague
- test gaps are identified
- missing guidance is flagged
