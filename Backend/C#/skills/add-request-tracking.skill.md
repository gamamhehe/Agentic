# Add Request Tracking Skill

## When to use

Adding endpoint-level telemetry, request logging, or Application Insights enrichment.

## Instructions to load

- `instructions/core/01-architecture.instructions.md`
- `instructions/core/02-naming.instructions.md`
- `instructions/layers/12-infrastructure.instructions.md`
- `instructions/layers/13-webapi.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md` — when tests in scope

## Patterns

- `patterns/logging.pattern.md`
- `patterns/api.pattern.md`

## Inputs

- Endpoint name, epic name, feature name
- Whether request/response body capture needed
- Sensitive data restrictions

## Steps

1. Confirm feature requires tracked telemetry
2. Telemetry implementation in Infrastructure; pipeline wiring in WebApi
3. Verify Application Insights registration in Infrastructure DI
4. Verify request logging middleware order in WebApi pipeline
5. Wire `WithApiTracking(...)` endpoint metadata and filter
6. Capture only needed telemetry
7. Avoid logging secrets or sensitive data
8. Suggest tests for middleware order and telemetry behavior

## Checklist

- [ ] WebApi only wires pipeline
- [ ] Infrastructure owns implementation
- [ ] Only tracked endpoints capture request bodies
- [ ] No sensitive data logged
- [ ] Middleware order correct
