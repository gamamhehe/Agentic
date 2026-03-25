# Build Use Case Skill

## When to use

Adding or updating an Application command, query, handler, or validator.

## Instructions to load

- `instructions/core/01-architecture.instructions.md`
- `instructions/core/02-naming.instructions.md`
- `instructions/layers/11-application.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md`
- `instructions/layers/10-domain.instructions.md` — when domain concepts involved
- `instructions/layers/12-infrastructure.instructions.md` — when new interfaces needed

## Patterns

- `patterns/application.pattern.md`

## Inputs

- Feature name
- Read or write intent
- Request fields
- Expected result shape
- Validation rules
- Infrastructure interfaces needed

## Steps

1. Decide command or query
2. Place request, handler, validator in correct feature folder
3. Define response DTOs in feature `Dtos/` folder when needed
4. Add FluentValidation rules
5. Depend only on Application interfaces — not Infrastructure implementations
6. Handler focused on orchestration — not transport or persistence details
7. Suggest unit tests for handler and validator

## Checklist

- [ ] Command/query naming correct
- [ ] Handler does not call another handler
- [ ] Validator co-located
- [ ] No Infrastructure namespace references
- [ ] DTO ownership correct
