---
name: write-tests
description: Add or update backend tests for C# and .NET features, changes, and regressions.
---

# Write Tests

Assume Codex has already read the repository `AGENTS.md`.

## When to use

Use this skill when the primary task is to add, update, or strengthen tests around changed backend behavior.

## Primary boundary

Lifecycle boundary: verification and regression coverage.

## Out of scope

- deciding business rules that are still undefined
- broad refactors unrelated to coverage
- PR-level approval decisions

## Typical inputs

- changed behavior or risk to cover
- target layer or component
- expected success path
- important failure, validation, or cancellation paths

## Workflow

1. Identify the behavior that changed or the risk that must stay protected.
2. Choose the narrowest test level that proves the behavior credibly.
3. Cover happy paths first, then meaningful validation or failure paths.
4. Keep tests readable, explicit, and aligned with repository conventions.
5. Call out any remaining gaps that need integration, contract, or operational testing.

## Output

- tests added or recommended
- behavior covered
- remaining risks or gaps
- verification notes

## Escalate to / pair with

- pair with the skill for the code under test
- pair with `review-backend-change` or `review-pull-request` when coverage gaps are the main finding
