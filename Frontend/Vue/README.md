# Frontend Guidance — Vue + Tailwind

AI guidance for Vue 3 + Tailwind CSS projects using GitHub Copilot.

Stack: **Vue 3**, **Tailwind CSS**

> **Work in progress.** Agent and stack guidance files will be added here.

---

## Two-tier model

| Tier              | Content                                 | Where it lives                                                         | When                         |
| ----------------- | --------------------------------------- | ---------------------------------------------------------------------- | ---------------------------- |
| **User space**    | `Frontend.agent.md` (orchestrator)      | `~/.github/agents/`                                                    | Installed once per machine   |
| **Project space** | `instructions/`, `skills/`, `patterns/` | `{repo}/.github/instructions/`, `.github/skills/`, `.github/patterns/` | Pulled per project on demand |

---

## Tier 1 — Install the agent to user space (one-time)

Copy the prompt below and paste it into any AI chat.
The AI will clone the repo, copy the agent files, write the entry point, and clean up.

> See the full prompt in the C# GitHub Copilot README under **Option 1** and **Option 2**.

After running, the result in user space will be:

```
~/.github/
  copilot-instructions.md
  agents/
    Backend.agent.md
    Frontend.agent.md
```

---

## Tier 2 — Pull stack guidance into a project (per repo)

Once stack guidance files exist in this repo, copy the prompt below and paste it into any AI chat.

> See the full prompt in the C# GitHub Copilot README under **Option 1**.

After running, the result in project space will be:

```
{workspaceRoot}/
  .github/
    copilot-instructions.md
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
```

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
