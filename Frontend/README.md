# Frontend AI Guidance

This folder contains AI guidance (agents, instructions, skills, patterns)
for frontend stacks.

## Stacks

| Stack              | Folder | Status                                             |
| ------------------ | ------ | -------------------------------------------------- |
| **Vue + Tailwind** | `Vue/` | Work in progress — see [Vue README](Vue/README.md) |

## Adding a new stack

Create a sub-folder named after the stack (e.g. `React/`, `Angular/`) mirroring
the structure of `Backend/C#/`. Add an agent, instructions, skills, patterns,
and a `copilot-instructions.md` entry point.

After cloning and running the install prompts, files land in the VS Code convention paths:

```
~/.github/                         ← user space (once per machine)
  copilot-instructions.md
  agents/
    Frontend.agent.md
  instructions/
    ...

{workspaceRoot}/.github/           ← project space (per repo)
  copilot-instructions.md
  agents/
    Frontend.agent.md
  instructions/
    ...
```
