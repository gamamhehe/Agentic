---
name: profile-current-backend-project
description: Profile an existing C# and .NET backend repository for architecture, testing, and governance gaps.
---

# Profile Current Backend Project

## When to use

Use this skill when the goal is to understand the current repository before implementation, refactoring, or governance work.

## Primary boundary

Lifecycle boundary: repository analysis and current-state profiling.

## Out of scope

- implementing feature changes
- refactoring code
- approving a pull request
- designing new business rules

## Typical inputs

- solution or repository root
- target scope when only one bounded context or service matters
- known problem areas when provided

## Workflow

1. Inventory the solution, projects, folders, and major dependencies.
2. Detect the actual layer structure and compare it to the expected backend architecture.
3. Identify configuration shape, auth surface, integrations, jobs, and data-access patterns.
4. Assess test posture across unit, application, and integration coverage.
5. Call out drift, risky conventions, missing observability, or missing governance decisions.
6. Summarize the current state in a way a lead can use to scope work.

## Output

- architecture snapshot
- detected conventions and deviations
- test posture summary
- operational and governance risk notes
- recommended next steps

## Escalate to / pair with

- pair with `review-backend-change` when the user wants a focused review of one risky area
- escalate to implementation skills only after profiling is complete
