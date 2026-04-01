---
name: Naming-Instructions
description: Standard naming patterns for projects, UseCase artifacts, endpoints, files, and C# identifiers.
applyTo: "**"
---

# Naming Instructions

## Project & Namespace Suffixes

| Layer             | Suffix               | Example                       |
| ----------------- | -------------------- | ----------------------------- |
| SharedKernel      | `.SharedKernel`      | `MyProject.SharedKernel`      |
| Domain            | `.Domain`            | `MyProject.Domain`            |
| Application       | `.Application`       | `MyProject.Application`       |
| Infrastructure    | `.Infrastructure`    | `MyProject.Infrastructure`    |
| WebApi            | `.WebApi`            | `MyProject.WebApi`            |
| Domain Tests      | `.Domain.Tests`      | `MyProject.Domain.Tests`      |
| Application Tests | `.Application.Tests` | `MyProject.Application.Tests` |
| Integration Tests | `.IntegrationTests`  | `MyProject.IntegrationTests`  |

## UseCase Artifacts

| Type | Pattern | Example |
| ---- | ------- | ------- |
| UseCase class | `{Verb}{Noun}` | `GetOrderById`, `UpsertOrder` |
| Request model | `Request` (nested class/record) | `GetOrderById.Request` |
| Response model | `Response` (nested class/record) | `GetOrderById.Response` |
| Validation class | `{UseCaseName}Validator` | `UpsertOrderValidator` |
| Boundary folder | `{BusinessContext}` | `Orders`, `Billing`, `Identity` |

## UseCase Interface Naming

| Scenario | Interface | Example |
| -------- | --------- | ------- |
| No input, no output | `ITaskUseCase` | `RebuildCache : ITaskUseCase` |
| One input, no output | `IUseCase<TRequest>` | `SendInvoice : IUseCase<Request>` |
| One input, output | `IUseCase<TRequest, TResponse>` | `SearchOrder : IUseCase<Request, Response>` |
| Two inputs, output | `IUseCase<TRequest1, TRequest2, TResponse>` | `UpsertOrder : IUseCase<Guid, Request, Guid>` |

## DTOs

| Type         | Pattern     | Example       |
| ------------ | ----------- | ------------- |
| Response DTO | `{Name}Dto` | `{Entity}Dto` |

## Endpoints

| Convention     | Rule                        | Example                |
| -------------- | --------------------------- | ---------------------- |
| Route path     | lowercase                   | `/api/v1/{entity}`     |
| `WithTags`     | PascalCase                  | `"{Entity}"`           |
| Endpoint name  | `Get{DomainModel}ById`      | `"Get{Entity}ById"`    |
| Endpoint class | `{DomainModel}Endpoints`    | `{Entity}Endpoints`    |
| Map method     | `Map{DomainModel}Endpoints` | `Map{Entity}Endpoints` |

## File Naming

| Type            | Pattern                    | Example                             |
| --------------- | -------------------------- | ----------------------------------- |
| UseCase         | `{UseCaseName}.cs`         | `SearchOrder.cs`                    |
| Validator       | `{UseCaseName}Validator.cs`| `UpsertOrderValidator.cs`           |
| Shared contract | `I{Name}.cs`               | `IUseCase.cs`, `IInteractor.cs`     |
| EF Core config  | `{Entity}Configuration.cs` | `{Entity}Configuration.cs`          |
| Repository      | `{Entity}Repository.cs`    | `{Entity}Repository.cs`             |
| Interface       | `I{Name}.cs`               | `I{Entity}Repository.cs`            |
| Extension class | `{Purpose}Extensions.cs`   | `OpenApiExtensions.cs`              |
| Cache service   | `{Entity}CacheService.cs`  | `{Entity}CacheService.cs`           |
| Background job  | `{Purpose}Job.cs`          | `ProcessDocumentJob.cs`             |

## C# Identifiers

- Classes, methods, properties: `PascalCase`
- Private fields: `_camelCase` (underscore prefix)
- Local variables and parameters: `camelCase`
- Constants: `PascalCase`
- Use primary constructor for classes with dependencies or immutable properties

## Business Context Grouping

- Group UseCases by business context boundary, not by HTTP endpoint or CRUD verb alone.
- Preferred folder pattern: `Application/Features/{BusinessContext}/UseCases/{UseCaseName}.cs`
- Preferred validator pattern: `Application/Features/{BusinessContext}/Validator/{UseCaseName}Validator.cs`
- Keep shared contracts for a context close to that context (`Dtos/`, `Contracts/`, or nested request/response types).

## SharedKernel Ownership

- Place `IUseCase`, `ITaskUseCase`, and `IInteractor` in `SharedKernel` project.
- Do not define duplicate `IUseCase` contracts inside Application or Infrastructure.
