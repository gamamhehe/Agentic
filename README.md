# Agentic — AI Guidance Repository

GitHub Copilot guidance organised by technology stack.
Uses a **two-tier model**: agent orchestrators live in your VS Code user space;
stack-specific guidance is pulled into each project on demand.

| Tier                         | What lives here                | Scope                          |
| ---------------------------- | ------------------------------ | ------------------------------ |
| **User space** `~/.github/`  | Agent files + root entry point | All workspaces, installed once |
| **Project space** `.github/` | Instructions, skills, patterns | Per repo, pulled on demand     |

## Stacks

| Stack              | Folder          | Guide                                     |
| ------------------ | --------------- | ----------------------------------------- |
| **C# / .NET**      | `Backend/C#/`   | [Backend README](Backend/C%23/README.md)  |
| **Vue + Tailwind** | `Frontend/Vue/` | [Frontend README](Frontend/Vue/README.md) |

## Repository layout

```
Backend/
  C#/
    agents/          <- agent file (copied to user space)
    instructions/    <- pulled into project on demand
    skills/
    patterns/
    copilot-instructions.md
Frontend/
  Vue/
    agents/          <- agent file (copied to user space)
    instructions/    <- pulled into project on demand (WIP)
    skills/
    patterns/
    copilot-instructions.md
skills/
  BootstrapAgenticGuidance.skill.md
README.md
```

---

## How to set up

See the guide in each stack's README:

- **Backend (C# / .NET)** → [`Backend/C#/README.md`](Backend/C%23/README.md)
- **Frontend (Vue + Tailwind)** → [`Frontend/Vue/README.md`](Frontend/Vue/README.md)

Or ask Copilot (once it is configured):

> _"Install the backend guidance into this project"_ > _"Pull the Vue stack guidance into this repo"_

Copilot will follow `skills/BootstrapAgenticGuidance.skill.md`.

---

## Precedence inside any stack

```
Instructions  >  Skills  >  Patterns
```
