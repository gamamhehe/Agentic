---
name: profile-current-backend-project
description: Profile an existing C# and .NET backend repository. Use when asked to assess the current project structure, risks, test posture, or missing Copilot guidance before implementation or refactoring.
---

# Profile Current Backend Project

## When to use

Use this skill when a lead or engineer wants Copilot to understand the current backend project before making changes, starting a refactor, or introducing guidance.

## Load this guidance

- `instructions/core/01-architecture.instructions.md`
- `instructions/core/02-naming.instructions.md`
- `instructions/core/03-csharp-code-style.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md`
- project instructions when they already exist

## Inputs

- solution or repository root
- target scope when the user wants only one bounded context or service
- known problem areas when provided

## Workflow

1. Inventory the solution, projects, folders, and major backend dependencies.
2. Detect the actual layer structure and compare it to the expected architecture.
3. Identify configuration shape, auth surface, integrations, background jobs, and data-access patterns.
4. Assess test posture across Domain, Application, and integration coverage.
5. Call out architecture drift, duplicated patterns, missing observability, or risky conventions.
6. Check whether project-specific guidance files exist and whether they are missing key decisions.
7. Summarize the current state in a way a lead can use to scope work or decide on refactors.

## Output

- current architecture snapshot
- detected conventions and deviations
- test posture summary
- configuration, integration, and operational risk notes
- missing guidance files or weak governance areas
- recommended next steps
