# Write Tests Skill

## When to use

Adding or updating tests for domain, application, integration, or API behavior.

## Load this additional guidance

Assume `@Backend-Engineer` has already loaded the core backend instructions.

- `instructions/cross-cutting/21-testing.instructions.md`
- layer instructions matching the code under test
- `instructions/project/team-standards.instructions.md` when local testing floors or naming rules exist

## Patterns

- `patterns/testing.pattern.md`
- `patterns/application.pattern.md` for handler tests
- `patterns/api.pattern.md` for integration or endpoint tests

## Inputs

- subject under test
- behavior to verify
- target test level
- dependencies to mock or keep real

## Steps

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

## Checklist

- [ ] Test level is appropriate
- [ ] Naming is consistent
- [ ] Tests are deterministic
- [ ] Assertions are meaningful
- [ ] Regression risk is covered
