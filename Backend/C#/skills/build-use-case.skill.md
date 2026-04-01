# Build Use Case Skill

## When to use

Adding or updating an Application UseCase and its request/response/validator contracts.

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

- business context name
- use case name
- request fields
- expected result shape
- validation rules
- infrastructure interfaces needed

## Steps

1. Define the business action and pick the proper `IUseCase` interface shape.
2. Place the UseCase under `Features/{BusinessContext}/UseCases/`.
3. Co-locate request/response contracts as nested types or context-level contracts.
4. Add FluentValidation rules under `Features/{BusinessContext}/Validator/` for externally supplied request data.
5. Keep `ExecuteAsync(...)` focused on orchestration, not transport or infrastructure details.
6. Use Application interfaces only; do not depend on Infrastructure implementations.
7. Ensure the UseCase is discoverable by automatic DI registration.
8. Suggest UseCase and validator tests when behavior is non-trivial.

## Output

- use case summary
- use case interface signature
- interfaces introduced or reused
- validation and test recommendations

## Checklist

- [ ] UseCase naming matches business action
- [ ] UseCase does not call another UseCase directly
- [ ] Validator is co-located
- [ ] Infrastructure dependencies are abstracted
- [ ] DTO ownership stays in Application
