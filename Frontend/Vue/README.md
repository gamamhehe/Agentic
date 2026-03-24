# Frontend Guidance — Vue + Tailwind

AI guidance for Vue 3 + Tailwind CSS projects using GitHub Copilot.

Stack: **Vue 3**, **Tailwind CSS**

> **Work in progress.** Agent and stack guidance files will be added here.

---

## Two-tier model

| Tier              | Content                                 | Where it lives                 | When                         |
| ----------------- | --------------------------------------- | ------------------------------ | ---------------------------- |
| **User space**    | `Frontend.agent.md` (orchestrator)      | `~/.github/Frontend/`          | Installed once per machine   |
| **Project space** | `instructions/`, `skills/`, `patterns/` | `{repo}/.github/Frontend/Vue/` | Pulled per project on demand |

---

## Tier 1 — Install the agent to user space (one-time)

Once the agent file exists in this repo, open Copilot Chat and ask:

> _"Install the frontend agent to my user space"_

Copilot will follow `skills/BootstrapAgenticGuidance.skill.md` — Step 1.

---

## Tier 2 — Pull stack guidance into a project (per repo)

Once stack guidance files exist in this repo, open the project in VS Code and ask:

> _"Pull the frontend stack guidance into this project"_

or

> _"Install the Vue guidance into this repo"_

---

## Planned structure

```
Frontend/Vue/
  agents/
    Frontend.agent.md
  instructions/
    Architecture.instructions.md
    Components.instructions.md
    Naming.instructions.md
    Styling.instructions.md
    Testing.instructions.md
  skills/
    CreateComponent.skill.md
    CreatePage.skill.md
    CreateComposable.skill.md
    WriteTests.skill.md
  patterns/
    ComponentPatterns.md
    ComposablePatterns.md
    TailwindPatterns.md
  copilot-instructions.md
  README.md
```
