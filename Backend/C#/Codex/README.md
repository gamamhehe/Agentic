# Codex Backend Guidance for C# / .NET

This pack adapts the current C# backend guidance to Codex conventions.

## What

This is the Codex-specific backend guidance pack for C# and .NET repositories.

It is built around:

- `AGENTS.md` as the main repository instruction surface
- shared repo-root domain reference sourced from `../domain-project.instructions.md`
- optional Codex skills under `skills/<skill-name>/SKILL.md`
- optional reference patterns under `patterns/`

This pack is for teams using Codex in the app, IDE extension, or CLI.

## Which

### Required

- `AGENTS.md`

Codex should read this file directly from the target repository root. This is the minimum install.

### Optional

- `domain-project.instructions.md`
- `skills/<skill-name>/SKILL.md`
- `patterns/*.pattern.md`

`domain-project.instructions.md` is the shared business-domain reference used by both Codex and GithubCopilot. Skills are optional workflow accelerators. Patterns are optional examples and are not required for installation.

## How

### Repository-local install

1. Clone this repository.
2. Copy `Backend/C#/Codex/AGENTS.md` into the target repository root as `AGENTS.md`.
3. Optionally copy `Backend/C#/domain-project.instructions.md` into the target repository root as `domain-project.instructions.md`.
4. Start using Codex in that repository.

If `<target-repo>/domain-project.instructions.md` already exists, do not replace it automatically. Ask whether to `replace`, `skip`, or `stop all`.

### Optional skill install

If you want reusable Codex workflows across repositories:

1. Pick the skill folders you want from `Backend/C#/Codex/skills/`.
2. Copy each folder into your user-level Codex skills directory.

### PowerShell copy example

```powershell
git clone https://github.com/gamamhehe/Agentic.git

Copy-Item .\Agentic\Backend\C#\Codex\AGENTS.md <target-repo>\AGENTS.md
Copy-Item .\Agentic\Backend\C#\domain-project.instructions.md <target-repo>\domain-project.instructions.md

Copy-Item -Recurse .\Agentic\Backend\C#\Codex\skills\review-pull-request $env:USERPROFILE\.codex\skills\
Copy-Item -Recurse .\Agentic\Backend\C#\Codex\skills\build-endpoint $env:USERPROFILE\.codex\skills\
```

### Copy checklist

- Copy `AGENTS.md` into the target repo root
- Optionally copy `domain-project.instructions.md` into the target repo root for shared business-domain rules
- If `domain-project.instructions.md` already exists in the target repo, do not overwrite it automatically
- Optionally copy selected skill folders into `~/.codex/skills/`
- Optionally keep `patterns/` nearby as reference docs

## Where

### Repository-local

- `<repo>/AGENTS.md`
- `<repo>/domain-project.instructions.md`

This is the recommended location for project-specific backend guidance.
`domain-project.instructions.md` is the recommended shared location for project-specific business language, aggregates, and invariants.

### User-level Codex locations

- `~/.codex/AGENTS.md`
- `~/.codex/skills/<skill-name>/SKILL.md`
- optional `~/.codex/config.toml`

### Windows examples

- `C:\Users\<User>\.codex\AGENTS.md`
- `C:\Users\<User>\.codex\skills\<skill-name>\SKILL.md`
- `C:\Users\<User>\.codex\config.toml`

## When

Use this Codex pack when:

- you are using Codex instead of GitHub Copilot
- you want repository behavior driven by `AGENTS.md`
- you want optional user-level skills that work across repositories

Use only repo-local `AGENTS.md` when:

- the repository needs a lightweight setup
- the team wants all important behavior defined in one file

Add repo-local `domain-project.instructions.md` when:

- the project has business terms, aggregates, invariants, or workflow rules that should be shared by Codex and GithubCopilot
- the team wants one domain source-of-truth instead of duplicating business rules in multiple tool packs

Install optional skills when:

- you repeat the same workflows across many repositories
- you want stronger support for review, refactor, profiling, bootstrap, or implementation tasks

## Who

### Team leads

Use `AGENTS.md` to define repository behavior, review expectations, approval gates, and required quality bars.
Use repo-root `domain-project.instructions.md` to define project-specific domain language and business rules.

### Backend engineers

Use the repo `AGENTS.md` every day, and add optional skills if you want reusable workflows across projects.

### Reviewers

Use `AGENTS.md` plus optional review skills such as:

- `review-backend-change`
- `review-pull-request`

### Bootstrap and setup owners

Use this README to install the minimum repo guidance and decide which optional skills belong in `~/.codex/skills/`.

## Sample target repo tree

```text
<target-repo>/
  AGENTS.md
  domain-project.instructions.md
  src/
  tests/
```

## Sample user-level skills tree

```text
~/.codex/
  skills/
    build-endpoint/
      SKILL.md
    review-pull-request/
      SKILL.md
    refactor-backend-feature/
      SKILL.md
```

## Available optional skills

- `profile-current-backend-project`
- `bootstrap-new-backend-project`
- `build-endpoint`
- `build-use-case`
- `update-domain-model`
- `build-infrastructure-dependency`
- `write-tests`
- `refactor-backend-feature`
- `review-backend-change`
- `review-pull-request`

Configuration, observability, feature-local use-case flow wiring, and fast merge-gate checks are covered inside the canonical skills above rather than exposed as separate top-level skills.

## GithubCopilot vs Codex

| Pack | Main entrypoint | Optional workflows | Install model |
| --- | --- | --- | --- |
| `GithubCopilot` | `.github/copilot-instructions.md` plus `.github/agents/` | `.github/skills/` and `.github/prompts/` | Copy into repo `.github/` |
| `Codex` | `AGENTS.md` | `~/.codex/skills/` | Copy `AGENTS.md` into repo root, optionally install user-level skills |

## Notes

- `AGENTS.md` is the only required runtime file in this pack.
- `domain-project.instructions.md` is the shared optional domain source for Codex and GithubCopilot.
- If the target repository already has `domain-project.instructions.md`, keep that local file unless replacement is explicitly approved.
- Skills are optional and should assume Codex reads `AGENTS.md` first.
- Patterns are reference material only and are not required for installation.
