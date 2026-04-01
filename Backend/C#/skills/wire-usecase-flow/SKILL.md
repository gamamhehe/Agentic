---
name: wire-usecase-flow
description: Set up or migrate automatic use-case registration and FluentValidation execution flow for a C# and .NET Application layer.
---

# Wire Use Case Flow

## When to use

Use this skill when setting up or migrating an Application layer to use-case execution with automatic DI registration and automatic FluentValidation integration.

## Load this guidance

- `instructions/layers/11-application.instructions.md`
- `instructions/layers/12-infrastructure.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md`
- `instructions/project/team-standards.instructions.md` when local completion rules exist

## Use these patterns as examples

- `patterns/application.pattern.md`
- `patterns/infrastructure.pattern.md`

## Inputs

- target Application assembly
- SharedKernel project availability
- SharedKernel `IUseCase` contract availability
- existing DI registration style
- validation strategy and exception mapping strategy

## Workflow

1. Confirm SharedKernel project exists or create `{ProjectName}.SharedKernel`.
2. Move shared execution contracts such as `IUseCase`, `ITaskUseCase`, and `IInteractor` to SharedKernel.
3. Update Application, Infrastructure, and WebApi references to use SharedKernel contracts.
4. Add assembly-scanning registration for all `IUseCase` implementations as scoped services.
5. Register FluentValidation validators from the Application assembly.
6. Add a use-case validation decorator or executor so validation runs automatically before `ExecuteAsync`.
7. Wire the extension from the Application composition root.
8. Ensure WebApi invokes use cases through interface injection or an interactor pattern.
9. Recommend tests for DI registration and validation flow behavior.

## Output

- integration summary
- new DI extension points
- validation flow behavior
- required package notes when Scrutor or FluentValidation packages are needed
- test recommendations
