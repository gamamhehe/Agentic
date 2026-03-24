# Copilot Instructions (Cross‑Project Template)

## Purpose

This file is the lightweight entry point for repository guidance.

Use `agents/Backend.agent.md` as the main orchestration guide.
That file explains how to select and apply instructions, skills, and patterns.

## Project Guidelines (customize)

- Language/runtime: .NET `{DotNetVersion}` (example: 10)
- Database: `{Database}` (example: Postgres)
- Background jobs: `{JobRunner}` (example: Hangfire)

> Replace the placeholders above with your project’s actual choices.

## Required Workflow

1. Follow `agents/Backend.agent.md`
2. Identify the task type and impacted layers
3. Load only the relevant instruction files
4. Load only the relevant skill files
5. Use the relevant pattern files as reference
6. For non-trivial work, provide a concise plan first
7. When the workflow requires approval before changes, wait for approval before implementing

## Precedence

When guidance overlaps or conflicts, use this order:

1. instructions
2. skills
3. patterns

Instructions define policy.
Skills define execution workflows.
Patterns provide implementation references.

## Review and Change Rules

- Do not assume all instruction files are relevant
- Do not duplicate instruction policy inside skills
- Do not let patterns override instructions
- If guidance is missing or contradictory, call it out and suggest an update
- Apply only safe, behavior-preserving IDE or Roslyn fixes unless explicitly asked for broader refactoring
- Avoid introducing newer syntax only for style if the repository does not already use it
