# Backend Guidance for C# / .NET

Structured GitHub Copilot guidance for backend engineering in C# and .NET projects.

Stack:

- C#
- .NET
- Entity Framework Core

---

## Purpose

This folder gives GitHub Copilot a backend operating model instead of only ad hoc prompts.

The backend guidance is designed around one rule:

- the backend agent is the main working surface

Instructions, skills, and patterns exist to support that agent.

---

## Guidance Model

This backend guidance follows a two-tier setup.

| Tier | Content | Location | Purpose |
| --- | --- | --- | --- |
| User space | `backend-engineer.agent.md` | `~/.github/agents/` | Makes the backend agent available across workspaces |
| Project space | `copilot-instructions.md`, `instructions/`, `skills/`, `patterns/` | `{workspaceRoot}/.github/` | Gives repo-specific backend context |

### Backend hierarchy

Use backend guidance in this order:

1. instructions
2. skills
3. patterns

Patterns are examples only.
They are not policy.

---

## Tier 1 - Install the backend agent once

Copy this prompt into an AI chat when you want the backend agent installed into GitHub user space:

```text
I want to set up backend GitHub Copilot guidance from https://github.com/gamamhehe/Agentic.git into my VS Code user space so it is available in every workspace.

Please do the following:

1. Clone the repo with a shallow clone (--depth 1) into a temporary directory.
2. Detect my OS:
   - Windows: %USERPROFILE%\\.github\\
   - Linux/macOS: ~/.github/
3. Create {userSpace}/agents/ if it does not exist.
4. Copy:
   - Backend/C#/agents/backend-engineer.agent.md -> {userSpace}/agents/Backend-Engineer.agent.md
5. Delete the temporary clone.
6. Show me the final tree under {userSpace}/.github/.
```

Expected result:

```text
~/.github/
  agents/
    Backend-Engineer.agent.md
```

---

## Tier 2 - Pull backend project guidance into a repo

Copy this prompt into an AI chat when you want backend guidance added to a specific project:

```text
I want to pull the backend C# / .NET GitHub Copilot guidance from https://github.com/gamamhehe/Agentic.git into this project.

Please do the following:

1. Clone the repo with a shallow clone (--depth 1) into a temporary directory.
2. Create these folders in the current workspace root if they do not exist:
   - .github/instructions/
   - .github/skills/
   - .github/patterns/
3. Copy:
   - Backend/C#/copilot-instructions.md -> .github/copilot-instructions.md
   - Backend/C#/instructions/* -> .github/instructions/   (preserve subfolders)
   - Backend/C#/skills/* -> .github/skills/
   - Backend/C#/patterns/* -> .github/patterns/
4. Delete the temporary clone.
5. Show me the final tree under .github/.
```

Expected result:

```text
{workspaceRoot}/
  .github/
    copilot-instructions.md
    instructions/
      core/
        01-architecture.instructions.md
        02-naming.instructions.md
      cross-cutting/
        20-configuration.instructions.md
        21-testing.instructions.md
      layers/
        10-domain.instructions.md
        11-application.instructions.md
        12-infrastructure.instructions.md
        13-webapi.instructions.md
      project/
        domain-project.instructions.template.md
        team-standards.instructions.template.md
    skills/
      add-request-tracking.skill.md
      build-endpoint.skill.md
      build-infrastructure-dependency.skill.md
      build-use-case.skill.md
      configure-application-settings.skill.md
      refactor-backend-feature.skill.md
      review-backend-change.skill.md
      review-pull-request.skill.md
      update-domain-model.skill.md
      write-tests.skill.md
    patterns/
      api.pattern.md
      application.pattern.md
      configuration.pattern.md
      domain.pattern.md
      entity-framework-core.pattern.md
      hangfire.pattern.md
      infrastructure.pattern.md
      logging.pattern.md
      structure.pattern.md
      testing.pattern.md
```

---

## How to work with it

Once the agent is installed and the project files are present:

1. Ask Copilot for a backend task in natural language.
2. Let `@Backend-Engineer` classify the task.
3. Let the agent decide which instructions and skills to load.
4. Use project instructions for domain-specific or team-specific refinements.

Examples:

| Task | Example prompt |
| --- | --- |
| Build endpoint | `Create an endpoint for GET /products` |
| Build use case | `Create a use case to place an order` |
| Update domain | `Add a Status property to the Order entity` |
| Infrastructure | `Implement IEmailSender with SendGrid` |
| Review local change | `Review this backend change for architecture and testing issues` |
| Review PR | `Review this pull request for regressions and merge risk` |
| Write tests | `Write tests for CreateOrderUseCase` |
| Refactor | `Refactor the payment feature to follow clean architecture` |

---

## Available backend files

### Agent

- `agents/backend-engineer.agent.md`

### Instructions

- `instructions/core/` for architecture and naming rules
- `instructions/layers/` for layer-specific constraints
- `instructions/cross-cutting/` for configuration and testing
- `instructions/project/` for project domain and team standards

### Skills

- `build-endpoint.skill.md`
- `build-use-case.skill.md`
- `update-domain-model.skill.md`
- `build-infrastructure-dependency.skill.md`
- `configure-application-settings.skill.md`
- `add-request-tracking.skill.md`
- `write-tests.skill.md`
- `refactor-backend-feature.skill.md`
- `review-backend-change.skill.md`
- `review-pull-request.skill.md`

### Patterns

Patterns are implementation references only.
Use them to shape code, not to define policy.

---

## Project customization

Keep `.github/copilot-instructions.md` minimal.

Prefer project-specific guidance in:

- `.github/instructions/project/domain-project.instructions.md`
- `.github/instructions/project/team-standards.instructions.md`

Use `domain-project` for business and model knowledge.
Use `team-standards` for review strictness, testing floor, and approval-required changes.

---

## Verification

After installing:

1. Open VS Code in a repo that has the backend project guidance.
2. Open Copilot Chat.
3. Ask: `What backend guidance do you have loaded?`

Expected behavior:

- Copilot identifies `Backend-Engineer` as the backend working surface
- Copilot mentions only the relevant instructions, skills, and patterns for the task

If it does not:

- confirm `~/.github/agents/Backend-Engineer.agent.md` exists
- confirm `.github/copilot-instructions.md` exists in the project
- confirm `github.copilot.chat.codeGeneration.useInstructionFiles` is enabled
- confirm VS Code is recent enough to support instruction files
