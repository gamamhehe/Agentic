---
name: build-endpoint
description: Create or update an HTTP endpoint in a C# and .NET backend.
---

# Build Endpoint

Assume Codex has already read the repository `AGENTS.md`.

## When to use

Use this skill when the primary change is to the HTTP transport surface: routes, endpoint handlers, request mapping, response mapping, and API metadata.

## Primary boundary

Transport/API boundary.

## Out of scope

- domain modeling
- infrastructure implementation
- project-wide DI architecture or bootstrap work
- broad refactors across multiple layers

## Typical inputs

- feature name
- route path and HTTP method
- request model or route and query parameters
- expected response model
- authorization requirements
- expected error cases

## Workflow

1. Confirm the behavior belongs in transport plus application orchestration, not in the endpoint itself.
2. Define or identify the use case the endpoint should call.
3. Keep the endpoint thin and explicit.
4. Apply metadata, error handling, and response declarations intentionally.
5. Keep validation and business rules outside the endpoint body.
6. Flag approval gates before introducing auth or contract changes.
7. Recommend success-path and failure-path tests.

## Output

- endpoint summary
- application contract used
- auth and validation notes
- recommended tests

## Escalate to / pair with

- pair with `build-use-case` when application orchestration is missing
- pair with `write-tests` for endpoint and contract coverage
