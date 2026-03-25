---
name: Application-Layer-Instructions
description: Rules for CQRS features, validators, DTO ownership, and interface boundaries.
applyTo: "**/*.Application/**"
---

# Application Layer Instructions

See `patterns/application.pattern.md` for code examples.

## Folder Structure

| Folder                                       | Purpose                                                          |
| -------------------------------------------- | ---------------------------------------------------------------- |
| `Common/Behaviors/`                          | MediatR pipeline behaviors (`ValidationBehavior`)                |
| `Common/Interfaces/`                         | Abstractions consumed by features, implemented in Infrastructure |
| `Common/Options/`                            | Strongly-typed configuration options                             |
| `Features/{Feature}/Queries/{QueryName}/`    | Query, handler, validator co-located                             |
| `Features/{Feature}/Commands/{CommandName}/` | Command, handler, validator co-located                           |
| `Features/{Feature}/Dtos/`                   | Response DTOs owned by that feature                              |
| `Utils/`                                     | Shared application-level utilities                               |

## CQRS Rules

- Every use-case is a Query (read) or Command (write)
- Each lives in its own sub-folder with exactly three files:
  - `{Name}.cs` — request record
  - `{Name}Handler.cs` — MediatR handler
  - `{Name}Validator.cs` — FluentValidation validator
- Handlers must not call other handlers directly
- Application must not reference Infrastructure namespaces

## DTO Ownership

- Response DTOs belong in `Features/{Feature}/Dtos/`
- DTOs must not be placed in Domain
- Request models are co-located with their handler

## Validation

- Use FluentValidation for all commands and queries
- Auto-discovered by `ValidationBehavior<TRequest, TResponse>` — never invoke manually
- Validator co-located with its command or query

## Interfaces

- All infrastructure dependencies abstracted behind interfaces in `Common/Interfaces/`
- Mirror folder structure to the implementing class in Infrastructure
- Interface naming: `I{Name}`

## Auth Abstractions

- Application defines `IUserContext` and similar abstractions
- Must not depend on ASP.NET Core HTTP or auth framework types directly
