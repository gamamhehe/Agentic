# Backend Guidance — C# / .NET

AI guidance for C# / .NET projects using GitHub Copilot.

Stack: **C#**, **.NET**, **Entity Framework Core**

---

## What is this?

This folder provides structured guidance that GitHub Copilot uses to assist with backend tasks.
It follows a **two-tier model**:

| Tier              | Content                                 | Where it lives               | When                         |
| ----------------- | --------------------------------------- | ---------------------------- | ---------------------------- |
| **User space**    | `Backend.agent.md` (orchestrator)       | `~/.github/Backend/`         | Installed once per machine   |
| **Project space** | `instructions/`, `skills/`, `patterns/` | `{repo}/.github/Backend/C#/` | Pulled per project on demand |

---

## Tier 1 — Install the agent to user space (one-time)

This makes the Backend agent available in **every VS Code workspace** on this machine.

### Ask Copilot

If you already have any `copilot-instructions.md` active, open Copilot Chat and ask:

> _"Install the backend agent to my user space"_

Copilot will follow `skills/BootstrapAgenticGuidance.skill.md` — Step 1.

### Result in user space

```
~/.github/
  copilot-instructions.md       <- entry point (references the agent)
  Backend/
    Backend.agent.md            <- orchestrator for all C# tasks
```

### Root `copilot-instructions.md` content

After the agent is installed, your `~/.github/copilot-instructions.md` should contain:

```markdown
## Backend (C#)

Use `Backend/Backend.agent.md` as the orchestrator for all backend tasks.
Stack-specific instructions, skills, and patterns are in `.github/Backend/C#/` inside the project repo.
```

---

## Tier 2 — Pull stack guidance into a project (per repo)

This pulls instructions, skills, and patterns into the open workspace so the agent
has full context for that specific project.

### Ask Copilot

Open the project in VS Code, open Copilot Chat, and ask:

> _"Pull the backend stack guidance into this project"_

or

> _"Install the C# guidance into this repo"_

Copilot will follow `skills/BootstrapAgenticGuidance.skill.md` — Step 2, and copy
the stack folders into `.github/Backend/C#/` inside the workspace.

### Result in project space

```
{workspaceRoot}/
  .github/
    Backend/
      C#/
        copilot-instructions.md
        instructions/
        skills/
        patterns/
```

---

## How to use

Once the agent (Tier 1) is in user space, Copilot is ready for backend tasks in any workspace.
Once the stack guidance (Tier 2) is pulled into a project, Copilot has full context for that repo.

Use natural language in Copilot Chat:

| Task                      | What to say                                                   |
| ------------------------- | ------------------------------------------------------------- |
| Create a new API endpoint | _"Create an endpoint for GET /products"_                      |
| Add a use case / command  | _"Create a use case to place an order"_                       |
| Update the domain model   | _"Add a Status property to the Order entity"_                 |
| Implement infrastructure  | _"Implement the IEmailSender with SendGrid"_                  |
| Review a change           | _"Review this change for architecture issues"_                |
| Write tests               | _"Write tests for the CreateOrderUseCase"_                    |
| Refactor a feature        | _"Refactor the payment feature to follow clean architecture"_ |

Copilot loads `Backend.agent.md`, selects the relevant skill, and applies the instructions and patterns.

---

## Customise for your project

After pulling stack guidance into a project, open `.github/Backend/C#/copilot-instructions.md`
and replace the placeholders:

```markdown
- Language/runtime: .NET `{DotNetVersion}` -> e.g. .NET 9
- Database: `{Database}` -> e.g. Postgres
- Background jobs: `{JobRunner}` -> e.g. Hangfire
```

For project-specific domain rules, edit `.github/Backend/C#/instructions/Domain.Project.Instructions.md`.

---

## Update guidance

To pull the latest version:

- **Agent:** ask Copilot _"Update the backend agent in my user space"_
- **Stack guidance:** ask Copilot _"Update the backend stack guidance in this project"_

---

## Verify

1. Open VS Code in any workspace.
2. Open Copilot Chat.
3. Ask: _"What guidance do you have loaded?"_

Copilot should mention `Backend.agent.md`.
If stack guidance is pulled into the project, it should mention the instruction files too.

If it does not:

- Confirm `~/.github/copilot-instructions.md` exists.
- Confirm VS Code setting `github.copilot.chat.codeGeneration.useInstructionFiles` is `true`.
- Confirm VS Code **1.93+** is installed.
