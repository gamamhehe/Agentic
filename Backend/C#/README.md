# Backend Guidance — C# / .NET

AI guidance for C# / .NET projects using GitHub Copilot.

Stack: **C#**, **.NET**, **Entity Framework Core**

---

## What is this?

This folder contains structured guidance that GitHub Copilot loads automatically
to assist with backend development tasks:

| Folder                    | Purpose                                                                  |
| ------------------------- | ------------------------------------------------------------------------ |
| `agents/`                 | Orchestrator — decides which guidance to load for each task              |
| `instructions/`           | Stable rules: architecture, naming, testing, domain, etc.                |
| `skills/`                 | Repeatable task workflows: create endpoint, use case, domain model, etc. |
| `patterns/`               | Implementation blueprints and code examples                              |
| `copilot-instructions.md` | Entry point Copilot reads when this is your active workspace             |

---

## Install

Choose one of the two methods below.

### Option A — Bash (Linux / macOS)

Installs guidance into your VS Code **user-level** config so it applies to all workspaces.

```bash
DEST="$HOME/.github/Backend/C#"
TMP=$(mktemp -d)
git clone --depth 1 https://github.com/gamamhehe/Agentic.git "$TMP"
mkdir -p "$DEST"
for f in agents instructions skills patterns; do
  src="$TMP/Backend/C#/$f"
  [ -d "$src" ] && cp -r "$src" "$DEST/"
done
cp "$TMP/Backend/C#/copilot-instructions.md" "$DEST/"
rm -rf "$TMP"
```

### Option B — PowerShell (Windows)

```powershell
$dest = "$env:USERPROFILE\.github\Backend\C#"
$tmp  = Join-Path $env:TEMP "agentic-$(Get-Random)"
git clone --depth 1 https://github.com/gamamhehe/Agentic.git $tmp
$src  = Join-Path $tmp "Backend\C#"
foreach ($f in @("agents","instructions","skills","patterns")) {
    $s = Join-Path $src $f ; $d = Join-Path $dest $f
    if (Test-Path $s) { New-Item $d -ItemType Directory -Force | Out-Null ; Copy-Item "$s\*" $d -Recurse -Force }
}
Copy-Item (Join-Path $src "copilot-instructions.md") $dest -Force
Remove-Item $tmp -Recurse -Force
```

### Option C — AI Agent (Copilot already active)

Open Copilot Chat and ask:

> _"Bootstrap the backend guidance"_

Copilot will follow `skills/BootstrapAgenticGuidance.skill.md` and run the install steps for you.

---

## Wire up the root entry point

GitHub Copilot reads a **single** `copilot-instructions.md` from `%USERPROFILE%\.github\`.
After installing, create or update that file so it points to this stack:

```markdown
# Copilot Instructions

## Backend (C#)

Follow guidance in `Backend/C#/copilot-instructions.md`.
Use `Backend/C#/agents/Backend.agent.md` as the orchestrator for all backend tasks.
```

> If you also have the Frontend stack installed, add a Frontend section to the same file.
> See [`Frontend/Vue/README.md`](../../Frontend/Vue/README.md).

---

## How to use

Once installed, Copilot automatically picks up the guidance. Use natural language in Copilot Chat:

| Task                      | What to say                                                   |
| ------------------------- | ------------------------------------------------------------- |
| Create a new API endpoint | _"Create an endpoint for GET /products"_                      |
| Add a use case / command  | _"Create a use case to place an order"_                       |
| Update the domain model   | _"Add a Status property to the Order entity"_                 |
| Implement infrastructure  | _"Implement the IEmailSender with SendGrid"_                  |
| Review a change           | _"Review this change for architecture issues"_                |
| Write tests               | _"Write tests for the CreateOrderUseCase"_                    |
| Refactor a feature        | _"Refactor the payment feature to follow clean architecture"_ |

Copilot will load the `Backend.agent.md` orchestrator, select the relevant skill,
and follow the instructions and patterns for that task.

---

## Customise for your project

Open `copilot-instructions.md` and replace the placeholders:

```markdown
- Language/runtime: .NET `{DotNetVersion}` -> e.g. .NET 9
- Database: `{Database}` -> e.g. Postgres
- Background jobs: `{JobRunner}` -> e.g. Hangfire
```

For project-specific domain rules, edit or replace `instructions/Domain.Project.Instructions.md`.

---

## Update guidance

Re-run the install script at any time to pull the latest version from the repo.
The `--depth 1` clone always fetches the latest default branch.

---

## Verify

1. Open VS Code in any workspace.
2. Open Copilot Chat.
3. Ask: _"What guidance do you have loaded?"_

Copilot should mention `Backend.agent.md` and the instruction files.

If it does not:

- Check that `%USERPROFILE%\.github\copilot-instructions.md` exists.
- Check that VS Code setting `github.copilot.chat.codeGeneration.useInstructionFiles` is `true`.
- Check that VS Code **1.93+** is installed.
