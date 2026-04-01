---
name: review-backend-change
description: Review a local backend change, staged patch, or focused code slice in a C# and .NET repository.
---

# Review Backend Change

## When to use

Use this skill when reviewing a local backend change, staged patch, or a focused code slice.

## Primary boundary

Lifecycle boundary: focused local review.

## Out of scope

- broad merge-gate approval across full PR context
- implementation work
- project bootstrap or repository profiling

## Typical inputs

- changed files or code slice
- intended behavior
- known risky areas
- whether the change is generated, manual, or mixed

## Workflow

1. Identify the intent and the touched boundaries.
2. Review correctness and architecture before style.
3. Check validation, error handling, async behavior, nullability, and data-access assumptions when relevant.
4. Check whether tests are missing for changed behavior.
5. Separate blocking issues from advisory cleanup.
6. Flag missing governance when the review reveals repeated confusion.

## Output

- prioritized findings with severity
- why each finding matters
- concrete fix direction
- missing test suggestions
- guidance gaps when present

## Escalate to / pair with

- escalate to `review-pull-request` when the user wants full merge-safety review across the whole PR
- pair with `write-tests` when missing coverage is the main issue
