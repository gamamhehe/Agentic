# Add Request Tracking Skill

## When to use

Adding endpoint-level telemetry, request logging, Application Insights enrichment, or request tracking metadata.

## Load this additional guidance

Assume `@Backend-Engineer` has already loaded the core backend instructions.

- `instructions/layers/12-infrastructure.instructions.md`
- `instructions/layers/13-webapi.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md` when tests are in scope
- `instructions/project/team-standards.instructions.md` when project observability rules exist

## Patterns

- `patterns/logging.pattern.md`
- `patterns/api.pattern.md`

## Inputs

- endpoint or feature name
- telemetry goals
- whether request or response bodies need to be captured
- sensitive data constraints

## Steps

1. Confirm tracking is required and what decision it should support.
2. Keep implementation in Infrastructure and pipeline wiring in WebApi.
3. Verify Application Insights and request tracking services are registered through Infrastructure DI.
4. Add endpoint metadata or filters only where tracking is required.
5. Capture only the minimum useful telemetry.
6. Avoid logging secrets, tokens, PII, or large payloads by default.
7. Suggest tests or verification steps for middleware order and telemetry behavior.

## Output

- summary of what was tracked
- files or layers affected
- sensitive-data decisions
- tests or verification steps

## Checklist

- [ ] WebApi only wires the pipeline
- [ ] Infrastructure owns the implementation
- [ ] Tracking is intentional, not global by accident
- [ ] Sensitive data is protected
- [ ] Verification or tests are suggested
