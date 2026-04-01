# Agentic

Reusable GitHub Copilot guidance packs organized by stack.

The backend C# pack in this repository is aligned to the official Copilot artifact model:

- custom agents
- repository and path-specific instructions
- agent skills
- reusable prompt files
- reference patterns

## Stacks

| Stack | Folder | Guide |
| --- | --- | --- |
| C# / .NET | `Backend/C#/` | [Backend README](Backend/C%23/README.md) |
| Vue + Tailwind | `Frontend/Vue/` | [Frontend README](Frontend/Vue/README.md) |

## Repository layout

```text
Backend/
  C#/
    agents/
    instructions/
    skills/
    prompts/
    patterns/
    copilot-instructions.md
Frontend/
  Vue/
    agents/
    instructions/
    skills/
    patterns/
    copilot-instructions.md
```

## Backend guidance model

The C# / .NET backend pack is built around these roles:

- `copilot-instructions.md` keeps the repository-wide baseline short and review-safe.
- `instructions/**/*.instructions.md` hold rules, constraints, and repository policy.
- `skills/<skill-name>/SKILL.md` hold repeatable workflows.
- `prompts/*.prompt.md` give leads and engineers reusable entrypoints for common tasks.
- `patterns/*.pattern.md` provide examples only.
- `agents/backend-engineer.agent.md` is the backend orchestrator for VS Code agent workflows.

## Setup

See the stack README for the installation prompt and the target `.github` layout:

- [Backend C# / .NET setup](Backend/C%23/README.md)
- [Frontend Vue setup](Frontend/Vue/README.md)

## Precedence inside a stack

```text
Instructions > Skills > Patterns
```

Prompt files are entrypoints. Agents orchestrate which instructions and skills to use.
