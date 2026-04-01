---
name: Backend-CSharp-Copilot-Instructions
description: Compact repository-wide baseline for C# and .NET backend work. Keep this file concise so it remains effective for coding and review surfaces.
applyTo: "**"
---

# Backend C# Copilot Instructions

Default to `@Backend-Engineer` for backend work in VS Code when the custom agent is available.

Use this file as the repository-wide baseline only. Keep detailed rules in `instructions/`, repeatable workflows in `skills/*/SKILL.md`, and examples in `patterns/`.

## Baseline

- Preserve clean layer boundaries: Domain and SharedKernel stay free of Infrastructure and WebApi concerns.
- Keep business logic out of endpoints, middleware, and infrastructure adapters.
- Prefer explicit C# and .NET code over implicit magic when behavior or failure handling matters.
- Treat nullability, cancellation, validation, configuration, logging, and test coverage as design responsibilities, not cleanup work.
- Use patterns as examples only. Patterns do not override instructions.

## Task Routing

- Coding and refactor work: use `agents/backend-engineer.agent.md` and the relevant layer instructions.
- Repeatable workflows: use the matching skill under `skills/<skill-name>/SKILL.md`.
- Review work: prioritize correctness, regression risk, architecture boundaries, contract safety, auth, configuration, data safety, and test evidence.

## Review Focus

- Block unsafe changes when changed behavior lacks tests, rollout notes, or operational safeguards.
- Keep review findings concise, risk-based, and actionable.
- Favor merge-risk findings over style-only feedback.

## Project Overrides

- Load the repository-root `domain-project.instructions.md` for local business rules.
- Load `instructions/project/team-standards.instructions.md` for team review thresholds, required tests, approval gates, and local coding preferences.

If repository-root `domain-project.instructions.md` already exists, treat it as the local source of truth and do not overwrite it automatically.
