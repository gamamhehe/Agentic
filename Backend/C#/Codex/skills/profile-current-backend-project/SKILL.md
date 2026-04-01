---
name: profile-current-backend-project
description: Profile the current C# and .NET backend repository to understand structure, risks, and missing governance.
---

# Profile Current Backend Project

Assume Codex has already read the repository `AGENTS.md`.

## When to use

Use this skill when the main goal is to understand the current repository before implementation, refactor, or review work.

## Primary boundary

Lifecycle boundary: current-project discovery and assessment.

## Out of scope

- implementing a feature change
- detailed refactoring of one subsystem
- PR-level approval decisions

## Typical inputs

- repository root
- solution and project layout
- dependency list
- configuration files
- existing tests and CI signals

## Workflow

1. Inspect the solution structure, layers, and main dependencies.
2. Identify architecture drift, coupling, and missing boundaries.
3. Review test posture, config shape, and operational concerns.
4. Note missing repository guidance, team standards, or review gates.
5. Summarize the highest-value next steps before implementation begins.

## Output

- architecture snapshot
- key risks and drift areas
- missing governance or guidance
- prioritized next-step recommendations

## Escalate to / pair with

- pair with `bootstrap-new-backend-project` when the main problem is missing baseline guidance
- pair with `review-backend-change` when the user wants findings on one focused slice of code
