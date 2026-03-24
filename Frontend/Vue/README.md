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

Copy the prompt below and paste it into any AI chat.
The AI will clone the repo, copy the agent files, write the entry point, and clean up.

> See the full prompt in [`skills/BootstrapAgenticGuidance.skill.md`](../../skills/BootstrapAgenticGuidance.skill.md)
> under **Prompt — Install agents to user space**.

---

## Tier 2 — Pull stack guidance into a project (per repo)

Once stack guidance files exist in this repo, copy the prompt below and paste it into any AI chat.

> See the full prompt in [`skills/BootstrapAgenticGuidance.skill.md`](../../skills/BootstrapAgenticGuidance.skill.md)
> under **Prompt — Pull frontend stack guidance into the current project**.

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
