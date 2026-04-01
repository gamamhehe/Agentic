# Agentic

Reusable AI guidance packs organized by stack and tool.

The C# backend guidance now has two tool-specific variants:

- GitHub Copilot
- Codex

## Stacks

| Stack | Folder | Guide |
| --- | --- | --- |
| C# / .NET | `Backend/C#/` | [C# chooser README](Backend/C%23/README.md) |
| Vue + Tailwind | `Frontend/Vue/` | [Frontend README](Frontend/Vue/README.md) |

## Repository layout

```text
Backend/
  C#/
    GithubCopilot/
    Codex/
Frontend/
  Vue/
    agents/
    instructions/
    skills/
    patterns/
    copilot-instructions.md
```

## C# backend variants

Use [Backend/C#/README.md](Backend/C%23/README.md) to choose the right backend pack:

- `GithubCopilot` for GitHub Copilot and `.github`-based repository guidance
- `Codex` for repository-local `AGENTS.md` plus optional `~/.codex/skills`

## Setup

See the stack README for the installation model and target layout:

- [Backend C# / .NET setup](Backend/C%23/README.md)
- [Frontend Vue setup](Frontend/Vue/README.md)

## Precedence inside a stack

```text
Instructions > Skills > Patterns
```

Prompt files are entrypoints. Agents orchestrate which instructions and skills to use.
