---
name: WebApi-Layer-Instructions
description: Guidelines for minimal API endpoints, OpenAPI, middleware, and WebApi boundaries.
applyTo: "**/*.WebApi/**"
---

# WebApi Layer Instructions

See `patterns/api.pattern.md` for endpoint and OpenAPI examples.

## Folder Structure

| Folder        | Purpose                                                     |
| ------------- | ----------------------------------------------------------- |
| `Endpoints/`  | Minimal API endpoint definitions grouped by feature         |
| `Extensions/` | `IServiceCollection` and `WebApplication` extension methods |
| `Middleware/` | Custom middleware (exception handling, API key auth)        |

## Minimal API Rules

- Route group paths: lowercase (`/api/v1/{domainmodel}`)
- `WithTags(...)`: PascalCase
- Use `TypedResults`, not `Results`
- Declare `.Produces<T>()` and `.ProducesProblem()` on every endpoint
- Endpoints are thin wrappers — no business logic
- Group endpoints by feature using `MapGroup`

## OpenAPI Rules

- Register via `AddOpenApiServices()` and `UseOpenApiPipeline()` extensions
- `OpenApiExtensions.cs` in `{ProjectName}.WebApi/Extensions/`
- Use Scalar for API reference UI
- Call `UseOpenApiPipeline()` after `UseAuthentication()` and `UseAuthorization()`
- Register document transformer for `Servers` and `Info`
- Register `AddApiHeaderParameter` operation transformer for API key header

## Middleware Rules

- Global exception handling in dedicated class under `Middleware/`
- API key auth in middleware, not endpoint filters
- All middleware registered in `Program.cs` via extension methods
- Request logging middleware: after `UseRouting()`, before `UseAuthentication()`
- Request logging implementation in `Infrastructure/ApplicationInsights/`

## Auth Extensions

- Authentication schemes and authorization policies in `AuthenticationExtensions.cs` under `Extensions/`
