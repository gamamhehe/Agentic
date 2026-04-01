---
name: write-tests
description: Add or update unit, application, integration, or API tests for a C# and .NET backend.
---

# Write Tests

## When to use

Use this skill when the primary task is to add or update tests.

## Primary boundary

Lifecycle boundary: verification and regression coverage.

## Out of scope

- designing business rules
- implementing primary production features from scratch
- broad review verdicts for a full PR

## Typical inputs

- subject under test
- behavior to verify
- target test level
- dependencies to mock or keep real

## Workflow

1. Choose the correct test level for the behavior and risk.
2. Place the test in the correct test project.
3. Keep setup minimal, deterministic, and easy to read.
4. Cover success, failure, and edge cases that matter to the change.
5. Avoid brittle assertions tied to incidental details.

## Output

- chosen test level
- scenarios covered
- dependencies mocked or kept real
- remaining test gaps if any

## Escalate to / pair with

- pair with the implementation skill for the code under test
- pair with `review-backend-change` when test gaps are discovered during review
