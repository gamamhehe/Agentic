# Bootstrap Agentic Guidance Skill

## When to use

Use this skill when the user wants to set up or refresh the AI guidance configuration
in a target project or in the VS Code user-level `.github` directory.

Typical trigger phrases:

- "set up the AI guidance"
- "install the Agentic config"
- "bootstrap Copilot instructions"
- "download and extract the Agentic repo"
- "configure AI guidance for this project"
- "install backend guidance"
- "install frontend guidance"
- "install both BE and FE guidance"

---

## Repository

```
https://github.com/gamamhehe/Agentic.git
```

Repo layout:

```
Backend/
  C#/
    agents/
    instructions/
    skills/
    patterns/
    copilot-instructions.md
Frontend/
  Vue/             <- Vue + Tailwind (add more stacks as sub-folders)
    agents/
    instructions/
    skills/
    patterns/
    copilot-instructions.md
skills/                <- shared / repo-level skills (this file lives here)
README.md
```

---

## Destination paths

| Scope                                            | Windows                    | Linux / macOS              |
| ------------------------------------------------ | -------------------------- | -------------------------- |
| **VS Code user-level** applies to ALL workspaces | `%USERPROFILE%\.github\`   | `~/.github/`               |
| **Project-level** applies only to this workspace | `{workspaceRoot}\.github\` | `{workspaceRoot}/.github/` |

> VS Code reads `copilot-instructions.md` from either location.
> User-level is the right choice when guidance should follow the developer across all projects.
> Project-level is the right choice when guidance is repo-specific.

---

## Inputs

Confirm with the user before running:

| Input                | Options                        | Default |
| -------------------- | ------------------------------ | ------- |
| **Stack**            | `backend`, `frontend`, `both`  | `both`  |
| **Destination**      | `user` or `project`            | `user`  |
| **Backend language** | `C#` (more may be added later) | `C#`    |
| **Frontend stack**   | `Vue`, `React`, `Angular`, ... | `Vue`   |
| **Overwrite**        | `yes` / `no`                   | `yes`   |

---

## Steps

### 1. Check prerequisites

```powershell
git --version
```

If `git` is not found, instruct the user to install it from https://git-scm.com and retry.

---

### 2. Resolve the destination root

**User-level (Windows):**

```powershell
$dest = "$env:USERPROFILE\.github"
if (-not (Test-Path $dest)) { New-Item -ItemType Directory -Path $dest | Out-Null }
```

**User-level (Linux / macOS):**

```bash
dest="$HOME/.github"
mkdir -p "$dest"
```

**Project-level:** use the workspace root folder instead of the above.

---

### 3. Clone the repo into a temp directory

```powershell
$tmp = Join-Path $env:TEMP "agentic-$(Get-Random)"
git clone --depth 1 https://github.com/gamamhehe/Agentic.git $tmp
```

---

### 4. Copy files Backend (C#)

Run this when stack is `backend` or `both`.

```powershell
$beStack = "C#"   # adjust if another backend language is added later
$beSrc   = Join-Path $tmp "Backend\$beStack"
$beDest  = Join-Path $dest "Backend\$beStack"

foreach ($f in @("agents", "instructions", "skills", "patterns")) {
    $s = Join-Path $beSrc $f
    $d = Join-Path $beDest $f
    if (Test-Path $s) {
        New-Item -ItemType Directory -Path $d -Force | Out-Null
        Copy-Item -Path "$s\*" -Destination $d -Recurse -Force
    }
}

$ci = Join-Path $beSrc "copilot-instructions.md"
if (Test-Path $ci) { Copy-Item $ci -Destination $beDest -Force }
```

---

### 5. Copy files Frontend

Run this when stack is `frontend` or `both`.
Replace `{FeStack}` with the user's chosen stack (e.g. `React`, `Vue`, `Angular`).

```powershell
$feStack = "Vue"   # change if using a different stack (React, Angular, ...)
$feSrc   = Join-Path $tmp "Frontend\$feStack"
$feDest  = Join-Path $dest "Frontend\$feStack"

foreach ($f in @("agents", "instructions", "skills", "patterns")) {
    $s = Join-Path $feSrc $f
    $d = Join-Path $feDest $f
    if (Test-Path $s) {
        New-Item -ItemType Directory -Path $d -Force | Out-Null
        Copy-Item -Path "$s\*" -Destination $d -Recurse -Force
    }
}

$ci = Join-Path $feSrc "copilot-instructions.md"
if (Test-Path $ci) { Copy-Item $ci -Destination $feDest -Force }
```

---

### 6. Write the root copilot-instructions.md

This is the **single entry point** GitHub Copilot reads.
Copy the repo root one if it exists, otherwise generate it:

```powershell
$rootCi = Join-Path $tmp "copilot-instructions.md"
if (Test-Path $rootCi) {
    Copy-Item $rootCi -Destination $dest -Force
} else {
    $content = @"
# Copilot Instructions

## Backend (C#)
Follow guidance in ``Backend/C#/copilot-instructions.md``.
Use ``Backend/C#/agents/Backend.agent.md`` as the orchestrator for all backend tasks.

## Frontend (Vue + Tailwind)
Follow guidance in ``Frontend/$feStack/copilot-instructions.md``.
Use ``Frontend/$feStack/agents/Frontend.agent.md`` as the orchestrator for all frontend tasks.
"@
    Set-Content -Path (Join-Path $dest "copilot-instructions.md") -Value $content -Encoding UTF8
}
```

If only one stack is installed, reference only that stack in the entry point.

---

### 7. Clean up

```powershell
Remove-Item -Path $tmp -Recurse -Force
```

---

### 8. Verify

```powershell
Get-ChildItem -Path $dest -Recurse | Select-Object FullName
```

---

## Wiring how Copilot resolves guidance

GitHub Copilot reads **one** `copilot-instructions.md` from:

1. `{workspaceRoot}/.github/copilot-instructions.md` project-level (takes precedence)
2. `%USERPROFILE%\.github\copilot-instructions.md` user-level (global fallback)

The root file at user-level should reference both stacks:

```markdown
# Copilot Instructions

## Backend (C#)

Follow guidance in `Backend/C#/copilot-instructions.md`.
Use `Backend/C#/agents/Backend.agent.md` as the orchestrator for all backend tasks.

## Frontend (Vue + Tailwind)

Follow guidance in `Frontend/Vue/copilot-instructions.md`.
Use `Frontend/Vue/agents/Frontend.agent.md` as the orchestrator for all frontend tasks.
```

For a **project-level** install, place only the relevant stack's `copilot-instructions.md`
directly at `{workspaceRoot}/.github/copilot-instructions.md`.

---

## Expected result after install (both stacks)

```
%USERPROFILE%\.github\
  copilot-instructions.md              <- root entry point
  Backend\
    C#\
      copilot-instructions.md
      agents\
        Backend.agent.md
      instructions\   (...)
      skills\         (...)
      patterns\       (...)
  Frontend\
    Vue\
      copilot-instructions.md
      agents\
        Frontend.agent.md
      instructions\   (...)
      skills\         (...)
      patterns\       (...)
```

---

## Verification

1. Open VS Code.
2. Start a Copilot Chat session.
3. Ask: _"What guidance do you have loaded?"_

Copilot should reference the root `copilot-instructions.md` and the relevant agent file.

If Copilot does not pick up the instructions, check:

- `copilot-instructions.md` exists at `%USERPROFILE%\.github\copilot-instructions.md`
- VS Code setting `github.copilot.chat.codeGeneration.useInstructionFiles` is `true`
- VS Code version is **1.93 or later** (user-level `.github` support was added in that release)

---

## Re-running / updating

Re-run steps 3-7 at any time to pull the latest guidance.
The `--depth 1` clone always fetches the latest default branch.
