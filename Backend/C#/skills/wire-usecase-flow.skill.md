# Wire UseCase Flow Skill

## When to use

Setting up or migrating an Application layer to UseCase execution with automatic DI registration and automatic FluentValidation integration.

## Load this additional guidance

Assume `@Backend-Engineer` has already loaded the core backend instructions.

- `instructions/layers/11-application.instructions.md`
- `instructions/layers/12-infrastructure.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md`
- `instructions/project/team-standards.instructions.md` when local completion rules exist

## Patterns

- `patterns/application.pattern.md`
- `patterns/infrastructure.pattern.md`

## Inputs

- target Application assembly
- SharedKernel project availability
- SharedKernel `IUseCase` contract availability
- existing DI registration style
- validation strategy and exception mapping strategy

## Steps

1. Confirm SharedKernel project exists (or create `{ProjectName}.SharedKernel`).
2. Move shared execution contracts (`IUseCase`, `ITaskUseCase`, `IInteractor`) to SharedKernel.
3. Update Application, Infrastructure, and WebApi references to use SharedKernel contracts.
4. Add assembly scanning extension to register all `IUseCase` implementations as scoped.
5. Register FluentValidation validators from Application assembly.
6. Add UseCase validation decorator/executor so validation runs automatically before `ExecuteAsync`.
7. Wire the extension from Application DI composition root.
8. Ensure WebApi invokes UseCases through interface injection or interactor/executor pattern.
9. Add tests for DI registration and validation flow behavior.

## Output

- integration summary
- new DI extension points
- validation flow behavior
- required package notes (if Scrutor/FluentValidation packages are needed)
- test recommendations

## Checklist

- [ ] SharedKernel project exists and is referenced by Application/Infrastructure/WebApi
- [ ] `IUseCase` and `IInteractor` contracts are located in SharedKernel
- [ ] All UseCase implementations are auto-registered
- [ ] No manual per-UseCase DI lines remain
- [ ] FluentValidation runs automatically in UseCase flow
- [ ] Validation failures map to expected API error shape
- [ ] Tests cover valid and invalid request paths