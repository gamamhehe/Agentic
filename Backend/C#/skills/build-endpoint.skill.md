# Build Endpoint Skill

## When to use

Adding or updating an HTTP endpoint in the WebApi layer.

## Instructions to load

- `instructions/core/01-architecture.instructions.md`
- `instructions/core/02-naming.instructions.md`
- `instructions/layers/13-webapi.instructions.md`
- `instructions/layers/11-application.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md` — when tests in scope

## Patterns

- `patterns/api.pattern.md`
- `patterns/application.pattern.md`

## Inputs

- Feature name, route, HTTP method
- Request model or parameters
- Expected response model
- Authorization requirements
- Error cases
- Whether a command or query is needed

## Steps

1. Confirm endpoint belongs in WebApi; business logic belongs outside
2. Define or identify the Application command/query the endpoint calls
3. Create or update endpoint group and route
4. Apply naming, route casing, tags, and OpenAPI metadata
5. Return `TypedResults`; declare `.Produces<T>()` and `.ProducesProblem()`
6. Validation handled in Application, not in endpoint
7. Add authorization and API key requirements when relevant
8. Suggest tests: success, validation failure, not-found, unauthorized

## Checklist

- [ ] Endpoint is thin — no business logic
- [ ] Route path lowercase, tags PascalCase
- [ ] `TypedResults` used
- [ ] OpenAPI metadata declared
- [ ] Command/query invoked via MediatR
