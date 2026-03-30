# Build Use Case Skill

## When to use

Adding or updating an Application command, query, handler, or validator.

## Load this additional guidance

Assume `@Backend-Engineer` has already loaded the core backend instructions.

- `instructions/layers/11-application.instructions.md`
- `instructions/layers/10-domain.instructions.md` when domain concepts or rules are involved
- `instructions/layers/12-infrastructure.instructions.md` when new interfaces are needed
- `instructions/cross-cutting/21-testing.instructions.md`
- `instructions/project/domain-project.instructions.md` when project domain rules exist
- `instructions/project/team-standards.instructions.md` when local completion rules exist

## Patterns

- `patterns/application.pattern.md`

## Inputs

- feature name
- read or write intent
- request fields
- expected result shape
- validation rules
- infrastructure interfaces needed

## Steps

1. Decide whether the use case is a command or query.
2. Place request, handler, and validator in the correct feature folder.
3. Define response DTOs in the feature `Dtos/` folder when needed.
4. Add FluentValidation rules for all externally supplied input.
5. Keep the handler focused on orchestration, not transport or infrastructure details.
6. Use Application interfaces only; do not depend on Infrastructure implementations.
7. Suggest handler and validator tests when behavior is non-trivial.

## Output

- use case summary
- command or query classification
- interfaces introduced or reused
- validation and test recommendations

## Checklist

- [ ] Command or query naming is correct
- [ ] Handler does not call another handler
- [ ] Validator is co-located
- [ ] Infrastructure dependencies are abstracted
- [ ] DTO ownership stays in Application
