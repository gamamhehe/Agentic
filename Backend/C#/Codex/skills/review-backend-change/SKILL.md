---
name: review-backend-change
description: Review a focused backend change in a C# and .NET repository for correctness, boundary safety, and missing tests.
---

# Review Backend Change

Assume Codex has already read the repository `AGENTS.md`.

## When to use

Use this skill when the primary task is reviewing a local patch, one feature slice, or a focused code change before merge.

## Primary boundary

Lifecycle boundary: local or slice-level review.

## Out of scope

- broad merge-gate approval across a full PR context
- implementation work unless explicitly requested after the review
- project profiling or bootstrap work

## Typical inputs

- changed files or diff
- intended behavior
- touched layers
- known risky behaviors such as auth, persistence, or config

## Workflow

1. Read the change intent before inspecting the diff.
2. Review correctness, regression risk, and boundary violations first.
3. Check for missing tests, risky config changes, and unclear behavior.
4. Keep findings tight and tied to concrete code locations or behaviors.
5. Separate blocking issues from follow-up suggestions.

## Output

1. `Findings`
2. `Test gaps`
3. `Open questions or assumptions`
4. `Short summary`

## Escalate to / pair with

- pair with `review-pull-request` when the task expands to full PR approval risk
- pair with `write-tests` when the main issue is missing coverage
