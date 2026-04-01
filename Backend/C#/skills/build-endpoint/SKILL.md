---
name: build-endpoint
description: Create or update an HTTP endpoint in a C# and .NET WebApi project. Use when asked to add, modify, or document a backend API endpoint.
---

# Build Endpoint

## When to use

Use this skill when adding or updating an HTTP endpoint in the WebApi layer.

## Load this guidance

- `instructions/layers/13-webapi.instructions.md`
- `instructions/layers/11-application.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md` when tests are in scope
- `instructions/project/team-standards.instructions.md` when local API or approval rules exist

## Use these patterns as examples

- `patterns/api.pattern.md`
- `patterns/application.pattern.md`

## Inputs

- feature name
- route path and HTTP method
- request model or route and query parameters
- expected response model
- authorization requirements
- expected error cases

## Workflow

1. Confirm the behavior belongs in WebApi plus Application, not in the endpoint itself.
2. Define or identify the use case the endpoint should call.
3. Create or update the endpoint group and route using established naming.
4. Apply OpenAPI metadata, response declarations, and endpoint naming.
5. Return `TypedResults` and keep transport logic thin.
6. Keep validation in Application, not in endpoint handlers.
7. Stop for approval before introducing new auth or approval-gated behavior.
8. Recommend API and use-case tests for success and failure paths.

## Output

- endpoint summary
- application contract used
- auth and validation notes
- recommended tests
