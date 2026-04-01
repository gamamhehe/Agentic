---
name: review-pull-request
description: Review a backend pull request, branch diff, or merge candidate in a C# and .NET repository with a correctness-first, merge-risk-focused workflow.
---

# Review Pull Request

## When to use

Use this skill when reviewing a backend pull request, branch diff, generated patch set, or pre-merge change set.

Primary goal: prevent unsafe merges and protect architectural integrity.

## Load this guidance

- `instructions/cross-cutting/21-testing.instructions.md`
- `instructions/cross-cutting/22-review-gates.instructions.md`
- `instructions/cross-cutting/23-pr-review.instructions.md`
- touched layer instructions
- `instructions/cross-cutting/20-configuration.instructions.md` when settings or options change
- `instructions/project/domain-project.instructions.md` when domain rules are relevant
- `instructions/project/team-standards.instructions.md` when local merge gates exist

## Inputs

- PR title and description
- changed files and diff
- intended behavior or acceptance criteria
- known risky areas such as auth, persistence, background jobs, or external integrations
- whether the PR changes contracts, config, or generated code

## Workflow

1. Read the PR goal first, then identify the touched layers and boundaries.
2. Review correctness and regression risk before style or cleanup suggestions.
3. Check architecture violations and layer leakage.
4. Check request, response, validation, contract, config, auth, migration, and operational risk.
5. Check async behavior, EF Core query behavior, transaction safety, cancellation, and concurrency risk when relevant.
6. Check tests for success paths, failure paths, regressions, and contract changes.
7. Separate blocking issues from advisory improvements.
8. Assign each critical finding to a merge-gate category from `22-review-gates.instructions.md`.
9. Flag missing guidance when the PR exposes repeated uncertainty or drift.

## Output

1. `Verdict`
2. `Blocking findings`
3. `Important non-blocking findings`
4. `Test gaps`
5. `Guidance gaps`

Each blocking finding should include the gate category, risk statement, and concrete fix direction.
