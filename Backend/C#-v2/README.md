# .NET Backend Guidance Kit

A cleaner guidance repository for AI-assisted .NET backend development.

This repository is organized so an AI agent can quickly understand:
- what each file type does
- which files to load first
- where rules live
- where workflows live
- where examples live

## Repository Layout

```text
.
├── agents/
│   └── backend-engineer.agent.md
├── instructions/
│   ├── core/
│   │   ├── 00-guidance-system.instructions.md
│   │   ├── 01-architecture.instructions.md
│   │   └── 02-naming.instructions.md
│   ├── layers/
│   │   ├── 10-domain.instructions.md
│   │   ├── 11-application.instructions.md
│   │   ├── 12-infrastructure.instructions.md
│   │   └── 13-webapi.instructions.md
│   ├── cross-cutting/
│   │   ├── 20-configuration.instructions.md
│   │   └── 21-testing.instructions.md
│   └── project/
│       └── Domain.Project.instructions.template.md
├── skills/
│   ├── add-request-tracking.skill.md
│   ├── build-endpoint.skill.md
│   ├── build-infrastructure-dependency.skill.md
│   ├── build-use-case.skill.md
│   ├── configure-application-settings.skill.md
│   ├── refactor-backend-feature.skill.md
│   ├── review-backend-change.skill.md
│   ├── update-domain-model.skill.md
│   └── write-tests.skill.md
├── patterns/
│   ├── api.pattern.md
│   ├── application.pattern.md
│   ├── configuration.pattern.md
│   ├── domain.pattern.md
│   ├── entity-framework-core.pattern.md
│   ├── hangfire.pattern.md
│   ├── infrastructure.pattern.md
│   ├── logging.pattern.md
│   ├── structure.pattern.md
│   └── testing.pattern.md
└── copilot-instructions.md
```

## Why this version is cleaner

- Adds a real entry point: `copilot-instructions.md`
- Adds a system-level instruction so the relationship between agent, instructions, skills, and patterns is explicit
- Separates **core**, **layer**, **cross-cutting**, and **project-specific** instructions
- Renames files so they are easier to scan and load
- Reduces policy duplication by putting “how the system works” in one place

## Old to New Mapping

See `migration-map.md`.
