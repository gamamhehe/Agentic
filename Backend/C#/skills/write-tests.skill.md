# Write Tests Skill

## When to use

Adding or updating tests for domain, application, integration, or API behavior.

## Instructions to load

- `instructions/core/02-naming.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md`
- Layer instructions matching code under test

## Patterns

- `patterns/testing.pattern.md`
- `patterns/application.pattern.md` — for handler test examples
- `patterns/api.pattern.md` — for integration test examples

## Inputs

- Subject under test
- Behavior to verify
- Test level (unit or integration)
- Dependencies to mock or keep real

## Steps

1. Choose correct test level
2. Place test in correct test project
3. Name class and methods using conventions
4. Keep setup minimal and deterministic
5. Mock only isolated dependencies
6. Cover success, failure, and edge cases
7. Avoid brittle assertions tied to incidental details

## Checklist

- [ ] Test level appropriate
- [ ] Naming consistent
- [ ] Tests deterministic
- [ ] Assertions meaningful
- [ ] Regression risk covered
