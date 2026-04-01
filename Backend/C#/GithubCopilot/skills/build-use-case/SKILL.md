---
name: build-use-case
description: Create or update application orchestration, request and response contracts, and validation in a C# and .NET backend.
---

# Build Use Case

## When to use

Use this skill when the primary change is application orchestration, use-case execution, request and response contracts, or validation flow.

## Primary boundary

Application orchestration boundary.

## Out of scope

- endpoint transport concerns
- infrastructure adapter implementation
- project bootstrap or project-wide setup
- pure domain modeling without orchestration changes

## Typical inputs

- business context name
- use case name
- request fields
- expected result shape
- validation rules
- interfaces needed from outer layers

## Workflow

1. Define the business action and choose the proper execution contract shape.
2. Co-locate request and response contracts with the use case or context.
3. Keep orchestration in the use case and push technical concerns outward.
4. Add validation rules for externally supplied request data.
5. Treat feature-local execution flow wiring as part of use-case work.
6. Recommend use-case and validator tests when behavior is non-trivial.

## Output

- use-case summary
- interface or execution signature
- interfaces introduced or reused
- validation and test recommendations

## Escalate to / pair with

- pair with `update-domain-model` when business rules change
- pair with `build-infrastructure-dependency` when new adapters or persistence are required
- pair with `write-tests` for use-case and validator coverage
