# Review Backend Change Skill

## When to use

Reviewing a backend change, pull request, or generated code.

## Instructions to load

- `instructions/core/01-architecture.instructions.md`
- `instructions/core/02-naming.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md`
- Layer instructions for touched layers

## Patterns

Only patterns relevant to touched code.

## Steps

1. Identify impacted layers and intent
2. Review architecture boundaries first
3. Review correctness and behavior risks
4. Review naming and structure consistency
5. Review validation, authorization, error handling
6. Review observability when relevant
7. Review test coverage and missing cases
8. Separate critical issues from optional improvements

## Output

- Prioritized findings with severity
- Explanation of why each matters
- Concrete fixes
- Missing test suggestions
- Guidance gap flags

## Checklist

- [ ] Architecture violations called out
- [ ] Correctness prioritized
- [ ] Review is concrete, not vague
- [ ] Test gaps identified
- [ ] Missing guidance flagged
