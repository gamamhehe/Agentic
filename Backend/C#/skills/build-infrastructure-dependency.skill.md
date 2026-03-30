# Build Infrastructure Dependency Skill

## When to use

Adding or updating persistence, caching, file storage, external API integration, telemetry, or background job infrastructure.

## Load this additional guidance

Assume `@Backend-Engineer` has already loaded the core backend instructions.

- `instructions/layers/12-infrastructure.instructions.md`
- `instructions/layers/11-application.instructions.md` when interfaces or application contracts change
- `instructions/cross-cutting/20-configuration.instructions.md` when config changes are needed
- `instructions/cross-cutting/21-testing.instructions.md`
- `instructions/project/team-standards.instructions.md` when approval gates or platform rules exist

## Patterns

- `patterns/infrastructure.pattern.md`
- `patterns/entity-framework-core.pattern.md` for EF Core work
- `patterns/hangfire.pattern.md` for background jobs
- `patterns/configuration.pattern.md` for options and binding

## Inputs

- dependency or technical concern to implement
- persistence or external service details
- configuration needs
- resiliency or observability needs

## Steps

1. Confirm the implementation belongs in Infrastructure.
2. Define or reuse the Application abstraction that Infrastructure will implement.
3. Implement the dependency in the correct Infrastructure location.
4. Register it through the correct DI concern in `DependencyInjection.cs`.
5. Add strongly-typed configuration when required.
6. Add logging, telemetry, retries, or error mapping intentionally.
7. Stop for approval before new external integrations, database schema work, or background jobs if the task is not already explicitly approved.
8. Suggest integration tests or focused unit tests.

## Output

- implemented dependency summary
- interface and DI changes
- config changes
- risk notes and test recommendations

## Checklist

- [ ] Implementation stays in Infrastructure
- [ ] Application depends only on abstractions
- [ ] DI registration is explicit and isolated by concern
- [ ] External failures are mapped intentionally
- [ ] Tests or verification steps are suggested
