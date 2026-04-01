# C# Backend Guidance Packs

This folder now contains two tool-specific guidance packs for C# and .NET backend work.

It also contains one shared project-domain file for C# and .NET only:

- `domain-project.instructions.md`

Keep that file at the target repository root only when the target repository is a C# or .NET backend and you want GithubCopilot and Codex to read the same business language, aggregate names, invariants, and workflow rules.

## Choose the right pack

### GithubCopilot

Use [GithubCopilot/README.md](GithubCopilot/README.md) when you want guidance built for GitHub Copilot and VS Code's `.github`-based instruction model.

This pack is centered on:

- `.github/copilot-instructions.md`
- `.github/agents/`
- `.github/instructions/`
- `.github/skills/`
- `.github/prompts/`
- `.github/patterns/`

### Codex

Use [Codex/README.md](Codex/README.md) when you want guidance built for Codex using repository-local `AGENTS.md` plus optional user-level skills in `~/.codex/skills`.

This pack is centered on:

- `<repo>/AGENTS.md`
- optional `~/.codex/skills/<skill-name>/SKILL.md`
- optional reference patterns

## Quick comparison

| Pack | Main runtime file | Optional reusable workflows | Best fit |
| --- | --- | --- | --- |
| `GithubCopilot` | `.github/copilot-instructions.md` plus `.github/agents/` | `.github/skills/` and `.github/prompts/` | GitHub Copilot and VS Code Agent mode |
| `Codex` | `AGENTS.md` | `~/.codex/skills/` | Codex app, IDE extension, or CLI |

## Folder map

```text
Backend/C#/
  README.md
  domain-project.instructions.md
  GithubCopilot/
  Codex/
```
