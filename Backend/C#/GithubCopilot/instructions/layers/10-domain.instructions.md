---
name: Domain-Layer-Instructions
description: Constraints for domain models, value objects, exceptions, and layer purity.
applyTo: "**/*.Domain/**"
---

# Domain Layer Instructions

See `patterns/domain.pattern.md` for code examples.

## Folder Structure

| Folder        | Purpose                                         |
| ------------- | ----------------------------------------------- |
| `Common/`     | Shared domain primitives (`Result<T>`, `Error`) |
| `Exceptions/` | Domain-specific exception types and error codes |
| `Models/`     | Business value objects and domain models        |
| `Utils/`      | Domain utility helpers (pure functions only)    |

## Allowed

- Business models and value objects
- Domain enums
- Domain exceptions and error codes
- Pure utility helpers with no external dependencies

## Forbidden

- Request or response DTOs
- API query models
- EF Core entities or persistence annotations (`[Table]`, `[Column]`)
- Persistence logic (`DbContext`, migrations, queries)
- External service response models
- References to Application, Infrastructure, or WebApi namespaces
- Third-party NuGet packages from outer layers
