---
name: Application-Layer-Instructions
description: Rules for UseCase features, validators, DTO ownership, and interface boundaries.
applyTo: "**/*.Application/**"
---

# Application Layer Instructions

See `patterns/application.pattern.md` for code examples.

## Folder Structure

| Folder | Purpose |
| ------ | ------- |
| `Features/{BusinessContext}/UseCases/` | UseCase classes grouped by business boundary |
| `Features/{BusinessContext}/Validator/` | FluentValidation validators for UseCase request types |
| `Common/Interfaces/` | Abstractions consumed by UseCases, implemented in Infrastructure |
| `Common/Options/` | Strongly-typed configuration options |
| `Common/Execution/` | Optional UseCase executors, decorators, and flow helpers |
| `Utils/` | Shared application-level utilities |

## UseCase Rules

- UseCases implement one of the `IUseCase` interfaces from SharedKernel.
- One UseCase class handles one business action and exposes `ExecuteAsync(...)`.
- Place UseCase by business context boundary (e.g., `Orders`, `Invoices`, `Users`).
- WebApi calls UseCases through an interactor/executor or directly by interface.
- UseCases must not call other UseCases directly.
- Application must not reference Infrastructure namespaces
- If `IUseCase` contracts currently exist in Application, move them to SharedKernel and update references.

## DTO Ownership

- Request/response contracts belong with the owning UseCase or business context.
- DTOs must not be placed in Domain
- Keep transport-specific HTTP models in WebApi; keep business request/response models in Application.

## Validation

- Use FluentValidation for all externally supplied UseCase inputs.
- Validators are auto-registered from Application assembly.
- Validation must run automatically in UseCase flow via decorator/executor, not manual calls in controllers.
- Prefer `IValidator<TRequest>` per request contract.

## DI Registration

- Register all `IUseCase` implementations automatically by assembly scanning.
- Register concrete UseCase class and exposed `IUseCase<...>` interface.
- Use `Scoped` lifetime for UseCases.
- Keep registration in one extension method (for example `AddUseCasesFromAssembly`).

## Interfaces

- All infrastructure dependencies abstracted behind interfaces in `Common/Interfaces/`
- Mirror folder structure to the implementing class in Infrastructure
- Interface naming: `I{Name}`

## Auth Abstractions

- Application defines `IUserContext` and similar abstractions
- Must not depend on ASP.NET Core HTTP or auth framework types directly
