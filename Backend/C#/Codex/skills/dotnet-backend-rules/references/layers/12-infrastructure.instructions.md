---
name: Infrastructure-Layer-Instructions
description: Implementation rules for persistence, adapters, caching, jobs, and DI.
applyTo: "**/*.Infrastructure/**"
---

# Infrastructure Layer Instructions

See `patterns/infrastructure.pattern.md` for DI, repository, cache, and adapter examples.
See `patterns/entity-framework-core.pattern.md` for audit and EF Core config.
See `patterns/hangfire.pattern.md` for background job examples.
See `patterns/logging.pattern.md` for telemetry setup.

## Folder Structure

| Folder                         | Purpose                                                  |
| ------------------------------ | -------------------------------------------------------- |
| `Caches/`                      | Cache services                                           |
| `Files/`                       | File handling (e.g. AzureBlobStorageService)             |
| `Services/`                    | Application interface implementations, external adapters |
| `Services/HangfireJobService/` | Background job classes (one per job)                     |
| `Persistence/`                 | ApplicationDbContext, DbContextFactory                   |
| `Persistence/Configurations/`  | EF Core `IEntityTypeConfiguration` classes               |
| `Persistence/Repositories/`    | Repository implementations                               |
| `Migrations/`                  | EF Core migration files                                  |
| `Migrations/DBScripts/`        | Idempotent SQL scripts                                   |
| `ApplicationInsights/`         | Telemetry middleware and filters                         |

## Implementation Rules

- Implement all interfaces from `Application/Common/Interfaces/`
- Never expose `DbContext` to Application — always use repositories
- `.AsNoTracking()` on all read queries
- `IEntityTypeConfiguration` for EF Core mappings — never in entity classes
- `DelegatingHandler` for injecting auth headers into HTTP clients
- `GetOrCreateAsync` for cache operations to prevent stampedes
- Wrap external APIs behind Application interfaces
- Map HTTP errors to domain exceptions — never propagate raw `HttpRequestException`

## Dependency Injection

`DependencyInjection.cs` rules:

- Single public `AddInfrastructureServices` method — orchestrates private sub-methods only
- Each sub-method: `private static void Add{Concern}(...)` — one concern each
- Never mix concerns in a sub-method
- Optional integrations silently skip when config is absent
- Do not manually register every UseCase class one-by-one; use assembly scanning extension for all `IUseCase` implementations

Current sub-methods:

| Method              | Concern                                          |
| ------------------- | ------------------------------------------------ |
| `AddDatabase`       | DbContext registration                           |
| `AddRepositories`   | Repository bindings                              |
| `AddCoreServices`   | IUserContext, HttpContextAccessor, core services |
| `AddHttpClients`    | Typed HttpClient registrations                   |
| `AddCaching`        | IMemoryCache configuration                       |
| `AddAuthentication` | JWT Bearer + authorization                       |
| `AddBlobStorage`    | Azure Blob Storage                               |
| `AddObservability`  | Application Insights + logging middleware        |
| `AddHangfire`       | Hangfire storage and server                      |

Adding a new concern:

1. Create `private static void Add{Concern}(...)` in `DependencyInjection.cs`
2. Call it from `AddInfrastructureServices`
3. Guard optional concerns with null/empty config check

## Background Jobs (Hangfire)

- One class per job under `Services/HangfireJobService/`
- Decorate with `[AutomaticRetry(Attempts = 3)]`
- Accept `IJobCancellationToken`, call `ThrowIfCancellationRequested()` at start
- **Simple variant**: constructor-inject singleton/transient deps
- **Scoped variant**: use `IServiceScopeFactory` + `CreateAsyncScope` for repositories
- **Recurring**: register via `UseHangfireJobs(this IHost host)` — call after `UseAuthorization()` and `UseHangfireDashboard()`
- **Fire-and-forget**: enqueue via `IBackgroundJobClient.Enqueue<TJob>(...)` from the triggering use-case
- See `patterns/hangfire.pattern.md` for complete examples

## Observability

- Telemetry implementation lives in `Infrastructure/ApplicationInsights/`
- Register via `AddObservability(...)` sub-method
- WebApi only adds middleware to pipeline — implementation stays in Infrastructure
- See `patterns/logging.pattern.md` for reference

## Audit Fields

- `CreatedBy` / `CreatedAt`: set once on creation, never overwritten
- `UpdatedBy` / `UpdatedAt`: set on every modification

## Auth Implementation

- Infrastructure provides `IUserContext` implementation
- Create `UserContextExtensions` for common transformations (`GetUserId()`)
