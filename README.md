# Agentic AI Guidance Repository

This repo contains GitHub Copilot guidance (agents, instructions, skills, patterns)
organised by technology stack. Each stack is self-contained and independently installable.

## Stacks

| Stack              | Folder          | Guide                                     |
| ------------------ | --------------- | ----------------------------------------- |
| **C# / .NET**      | `Backend/C#/`   | [Backend README](Backend/C%23/README.md)  |
| **Vue + Tailwind** | `Frontend/Vue/` | [Frontend README](Frontend/Vue/README.md) |

## Repository layout

```
Backend/
  C#/                  <- C# / .NET guidance
    agents/
    instructions/
    skills/
    patterns/
    copilot-instructions.md
    README.md
Frontend/
  Vue/                 <- Vue + Tailwind guidance (work in progress)
    README.md
skills/                <- shared / repo-level skills
  BootstrapAgenticGuidance.skill.md
README.md              <- this file
```

---

## Detailed guides

- **Backend (C# / .NET)** [`Backend/C#/README.md`](Backend/C%23/README.md)
  Full install and usage guide for the C# / .NET stack.

- **Frontend (Vue + Tailwind)** [`Frontend/Vue/README.md`](Frontend/Vue/README.md)
  Work in progress.

---

## Shared bootstrap skill

If Copilot is already configured in your editor, ask it:

> _"Bootstrap the Agentic guidance"_

Copilot will follow `skills/BootstrapAgenticGuidance.skill.md` and walk you through
installing whichever stacks you need.

---

## Precedence inside any stack

```
Instructions  >  Skills  >  Patterns
```

Instructions define policy. Skills define execution workflows. Patterns provide implementation references.
