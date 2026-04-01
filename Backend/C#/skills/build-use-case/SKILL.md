---
name: build-use-case
description: Create or update an Application use case, request and response contracts, and validators in a C# and .NET backend.
---

# Build Use Case

## When to use

Use this skill when adding or updating an Application use case and its request, response, and validator contracts.

## Load this guidance

- `instructions/layers/11-application.instructions.md`
- `instructions/layers/10-domain.instructions.md` when domain concepts or rules are involved
- `instructions/layers/12-infrastructure.instructions.md` when new interfaces are needed
- `instructions/cross-cutting/21-testing.instructions.md`
- `instructions/project/domain-project.instructions.md` when project domain rules exist
- `instructions/project/team-standards.instructions.md` when local completion rules exist

## Use these patterns as examples

- `patterns/application.pattern.md`

## Inputs

- business context name
- use case name
- request fields
- expected result shape
- validation rules
- infrastructure interfaces needed

## Workflow

1. Define the business action and pick the proper `IUseCase` interface shape.
2. Place the use case under `Features/{BusinessContext}/UseCases/`.
3. Co-locate request and response contracts as nested types or context-level contracts.
4. Add FluentValidation rules under `Features/{BusinessContext}/Validator/` for externally supplied request data.
5. Keep `ExecuteAsync(...)` focused on orchestration, not transport or infrastructure details.
6. Use Application interfaces only and do not depend on Infrastructure implementations.
7. Ensure the use case is discoverable by automatic DI registration.
8. Recommend use-case and validator tests when behavior is non-trivial.

## Output

- use-case summary
- interface signature
- interfaces introduced or reused
- validation and test recommendations
