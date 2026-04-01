---
name: write-tests
description: Add or update unit, application, integration, or API tests for a C# and .NET backend.
---

# Write Tests

## When to use

Use this skill when adding or updating tests for domain, application, integration, or API behavior.

## Load this guidance

- `instructions/cross-cutting/21-testing.instructions.md`
- layer instructions matching the code under test
- `instructions/project/team-standards.instructions.md` when local testing floors or naming rules exist

## Use these patterns as examples

- `patterns/testing.pattern.md`
- `patterns/application.pattern.md` for use-case tests
- `patterns/api.pattern.md` for integration or endpoint tests

## Inputs

- subject under test
- behavior to verify
- target test level
- dependencies to mock or keep real

## Workflow

1. Choose the correct test level for the behavior and risk.
2. Place the test in the correct test project.
3. Follow test naming conventions consistently.
4. Keep setup minimal, deterministic, and easy to read.
5. Mock only what should be isolated.
6. Cover success, failure, and edge cases that matter to the change.
7. Avoid brittle assertions tied to incidental details.

## Output

- chosen test level
- scenarios covered
- dependencies mocked or kept real
- remaining test gaps if any
