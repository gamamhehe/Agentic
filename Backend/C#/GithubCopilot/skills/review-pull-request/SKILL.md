---
name: review-pull-request
description: Review a backend pull request or merge candidate in a C# and .NET repository with a correctness-first, merge-risk-focused workflow.
---

# Review Pull Request

## When to use

Use this skill when the primary task is PR review, merge-safety review, or a fast merge-gate decision.

## Primary boundary

Lifecycle boundary: PR-level review and approval risk.

## Out of scope

- implementation work
- local pre-implementation review minutiae unless the user explicitly narrows to one code slice
- project bootstrap or profiling

## Typical inputs

- PR title and description
- changed files and diff
- intended behavior or acceptance criteria
- known risky areas such as auth, persistence, background jobs, or external integrations
- whether the PR changes contracts, config, or generated code

## Workflow

1. Read the PR goal first, then identify the touched boundaries.
2. Review correctness and regression risk before cleanup suggestions.
3. Check architecture, contracts, config, auth, migration, and operational risk.
4. Treat fast merge-gate checks as a review mode of this skill, not a separate skill.
5. Check tests for success paths, failure paths, regressions, and contract changes.
6. Separate blocking issues from advisory improvements.
7. Flag missing governance when the PR exposes repeated uncertainty or drift.

## Output

1. `Verdict`
2. `Blocking findings`
3. `Important non-blocking findings`
4. `Test gaps`
5. `Guidance gaps`

## Escalate to / pair with

- pair with `review-backend-change` only when the user wants deep inspection of one code slice
- pair with `write-tests` when the main remediation is missing coverage
