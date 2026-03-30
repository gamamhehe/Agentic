# Review Pull Request Skill

## When to use

Reviewing a backend pull request, branch diff, generated patch set, or pre-merge change set.

## Load this additional guidance

Assume `@Backend-Engineer` has already loaded the core backend instructions.

- `instructions/cross-cutting/21-testing.instructions.md`
- layer instructions for touched layers
- `instructions/cross-cutting/20-configuration.instructions.md` when settings or options change
- `instructions/project/domain-project.instructions.md` when domain rules are relevant
- `instructions/project/team-standards.instructions.md` when local merge gates exist

## Patterns

Only patterns relevant to touched code.

## Inputs

- PR title and description
- changed files and diff
- intended behavior or acceptance criteria
- known risky areas such as auth, persistence, background jobs, or external integrations
- whether the PR changes contracts, config, or generated code

## Steps

1. Read the PR goal first, then identify the touched layers and boundaries.
2. Review correctness and regression risk before style or cleanup suggestions.
3. Check architecture violations and layer leakage.
4. Check request, response, validation, and contract risk.
5. Check operational risk for auth, configuration, integrations, observability, and background jobs.
6. Check async behavior, EF Core query behavior, transaction safety, and concurrency risk when relevant.
7. Check tests for success paths, failure paths, regressions, and contract changes.
8. Separate blocking issues from advisory improvements.
9. Flag missing guidance when the PR exposes repeated uncertainty or drift.

## Output

- short PR intent summary
- prioritized findings with severity
- why each issue matters
- concrete fix direction
- missing or weak test cases
- guidance gap notes when relevant

## Checklist

- [ ] Correctness is reviewed before style
- [ ] Architecture boundary violations are called out
- [ ] Contract and merge-risk issues are identified
- [ ] Operational and async risks are checked when relevant
- [ ] Test gaps are concrete
- [ ] Findings are actionable
