---
name: Backend-CSharp-Copilot-Instructions
description: Lightweight backend entrypoint for C#/.NET repositories. Route to Backend-Engineer and relevant instruction and skill files.
applyTo: "**"
---

# Backend C# Copilot Instructions

Use `@Backend-Engineer` as the default working surface for backend tasks.

Keep this file lightweight. It is a router, not a full rulebook.

## Load Order

1. `agents/backend-engineer.agent.md`
2. `instructions/core/01-architecture.instructions.md`
3. `instructions/core/02-naming.instructions.md`
4. `instructions/core/03-csharp-code-style.instructions.md`
5. Layer instructions that match touched code
6. Cross-cutting instructions that match the task
7. Matching skill
8. Patterns only as examples

## Always Load for Review Tasks

- `instructions/cross-cutting/21-testing.instructions.md`
- `instructions/cross-cutting/22-review-gates.instructions.md`

## Quick Skill Routing

- Endpoint work -> `skills/build-endpoint.skill.md`
- Use-case work -> `skills/build-use-case.skill.md`
- Use-case DI and validation flow wiring -> `skills/wire-usecase-flow.skill.md`
- Domain changes -> `skills/update-domain-model.skill.md`
- Infrastructure/integrations -> `skills/build-infrastructure-dependency.skill.md`
- Config work -> `skills/configure-application-settings.skill.md`
- Local change review -> `skills/review-backend-change.skill.md`
- PR review -> `skills/review-pull-request.skill.md`
- PR protection and merge gate check -> `skills/protect-backend-project.skill.md`

## Guardrails

- Prefer correctness, architecture boundaries, and regression prevention over style-only edits.
- Do not approve risky changes without explicit test and operational coverage.
- If a repeated issue appears, propose instruction or skill updates.
