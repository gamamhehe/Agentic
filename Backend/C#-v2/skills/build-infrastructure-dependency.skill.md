# Implement Infrastructure Dependency Skill

> Cross‑project note: replace placeholders like `{Entity}` and `{ProjectName}` with real names.

## When to use

Use this skill when the task adds or updates persistence, caching, storage, external API integration, telemetry wiring, or other Infrastructure implementations.

Typical cases:

- implement an Application interface
- add an EF Core repository or configuration
- add a typed HTTP client or adapter
- add blob or file storage implementation
- add a recurring Hangfire job class and register it via UseHangfireJobs
- add a fire-and-forget Hangfire job enqueued via IBackgroundJobClient

## Relevant instructions

Usually load:

- `instructions/core/01-architecture.instructions.md`
- `instructions/layers/12-infrastructure.instructions.md`
- `instructions/core/02-naming.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md`

Load `instructions/layers/11-application.instructions.md` when new interfaces or options are defined there.
Load `instructions/cross-cutting/20-configuration.instructions.md` when configuration changes are needed.

## Related patterns

Use as reference:

- `patterns/infrastructure.pattern.md`
- `patterns/entity-framework-core.pattern.md`
- `patterns/domain.pattern.md`
- `patterns/configuration.pattern.md` when options are involved
- `patterns/hangfire.pattern.md` when adding background jobs

## Inputs

- interface or technical concern to implement
- persistence or external service details
- configuration needs
- resiliency or observability needs

## Steps

1. Confirm the implementation belongs in Infrastructure
2. Implement the Application interface or technical component in the correct folder
3. Register the dependency in Infrastructure DI
4. Keep Application free from Infrastructure types and concerns
5. Add configuration or options binding if needed
6. Consider logging, telemetry, retries, and error mapping where relevant
7. For Hangfire jobs: place the class in Services/HangfireJobService/, decorate with [AutomaticRetry], use IServiceScopeFactory for scoped deps, register recurring jobs via UseHangfireJobs and fire-and-forget jobs via IBackgroundJobClient at the call site
8. Suggest integration tests or targeted unit tests

## Output

- Infrastructure implementation
- DI registration
- settings updates when needed
- test recommendations

## Checklist

- implementation stays in Infrastructure
- Application only depends on abstraction
- DI registration is added
- external failures are mapped intentionally
- configuration is strongly typed when needed
- Hangfire job classes decorated with [AutomaticRetry] and placed under Services/HangfireJobService/
- Scoped variant used (IServiceScopeFactory) when repositories or scoped services are needed
- Recurring jobs: UseHangfireJobs called in Program.cs after UseAuthorization() and UseHangfireDashboard()
- Fire-and-forget jobs: enqueued via IBackgroundJobClient from the triggering use-case or service
