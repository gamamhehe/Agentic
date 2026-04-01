---
name: bootstrap-new-backend-project
description: Set up the initial Copilot guidance pack for a new C# and .NET backend repository. Use when a team wants to enable consistent implementation, refactoring, and PR review from the start.
---

# Bootstrap New Backend Project

## When to use

Use this skill when setting up backend Copilot guidance for a fresh C# and .NET repository or for a repository that has no meaningful local guidance yet.

## Load this guidance

- `copilot-instructions.md`
- `agents/backend-engineer.agent.md`
- `instructions/core/01-architecture.instructions.md`
- `instructions/core/02-naming.instructions.md`
- `instructions/core/03-csharp-code-style.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md`
- `instructions/cross-cutting/22-review-gates.instructions.md`
- `instructions/project/domain-project.instructions.template.md`
- `instructions/project/team-standards.instructions.template.md`

## Inputs

- repository root
- solution or project naming choice
- whether the repo already has Domain, Application, Infrastructure, WebApi, and SharedKernel projects
- team preferences or governance requirements when provided

## Workflow

1. Create the `.github` guidance structure needed for backend work.
2. Install the backend custom agent, repository baseline instructions, path-specific instructions, skills, prompts, and patterns.
3. Copy the project instruction templates that need real repository decisions.
4. Explain which files are ready to use immediately and which must be tailored by the team lead.
5. Call out missing architectural pieces such as SharedKernel, test projects, or solution layout if the repo is incomplete.
6. Return a short follow-up checklist for filling project-specific rules.

## Output

- installed guidance summary
- files copied or created
- project-specific files that still need decisions
- gaps between the current repo structure and the expected backend architecture
