# Build Infrastructure Dependency Skill

## When to use

Adding or updating persistence, caching, storage, external API integration, telemetry, or background jobs.

## Instructions to load

- `instructions/core/01-architecture.instructions.md`
- `instructions/core/02-naming.instructions.md`
- `instructions/layers/12-infrastructure.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md`
- `instructions/layers/11-application.instructions.md` — when new interfaces needed
- `instructions/cross-cutting/20-configuration.instructions.md` — when config changes needed

## Patterns

- `patterns/infrastructure.pattern.md`
- `patterns/entity-framework-core.pattern.md` — for EF Core work
- `patterns/hangfire.pattern.md` — for background jobs
- `patterns/configuration.pattern.md` — for options binding

## Inputs

- Interface or technical concern to implement
- Persistence or external service details
- Configuration needs
- Resiliency or observability needs

## Steps

1. Confirm implementation belongs in Infrastructure
2. Implement interface or component in correct folder
3. Register dependency in Infrastructure DI (new sub-method if new concern)
4. Keep Application free from Infrastructure types
5. Add configuration/options binding if needed
6. Consider logging, telemetry, retries, error mapping
7. For Hangfire jobs: place in `Services/HangfireJobService/`, use `[AutomaticRetry]`, use `IServiceScopeFactory` for scoped deps
8. Suggest integration tests or targeted unit tests

## Checklist

- [ ] Implementation stays in Infrastructure
- [ ] Application depends only on abstraction
- [ ] DI registration added
- [ ] External failures mapped intentionally
- [ ] Configuration strongly typed when needed
- [ ] Hangfire: `[AutomaticRetry]`, correct variant (simple vs scoped)
- [ ] Recurring jobs registered via `UseHangfireJobs`
- [ ] Fire-and-forget via `IBackgroundJobClient`
