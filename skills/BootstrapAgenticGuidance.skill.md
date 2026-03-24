# Bootstrap Agentic Guidance Skill

## When to use

Use this skill when the user wants to set up or install AI guidance from the Agentic repo.

Typical trigger phrases:

- "set up the AI guidance"
- "install the Agentic config"
- "bootstrap Copilot instructions"
- "configure AI guidance for this project"
- "install backend guidance"
- "install frontend guidance"
- "install both BE and FE guidance"
- "pull the backend stack into this project"
- "pull the frontend stack into this project"

---

## Architecture  two-tier install model

Guidance is split into two tiers with different scopes and install targets.

```
Tier 1  User space (installed once, applies to ALL workspaces)
  %USERPROFILE%\.github\                  (Windows)
  ~/.github/                              (Linux / macOS)
    copilot-instructions.md              <- root entry point
    Backend\
      Backend.agent.md                   <- BE orchestrator
    Frontend\
      Frontend.agent.md                  <- FE orchestrator

Tier 2  Project space (pulled per project, lives inside the repo)
  {workspaceRoot}\.github\
    Backend\C#\
      instructions\   <- C# rules
      skills\         <- C# task workflows
      patterns\       <- C# blueprints
    Frontend\Vue\
      instructions\   <- Vue + Tailwind rules
      skills\         <- Vue task workflows
      patterns\       <- Vue blueprints
```

**Agents** (Tier 1) are stable orchestrators that live in user space and work across all projects.
**Stack guidance** (Tier 2) is project-specific and pulled into the repo on demand.

---

## Repository

```
https://github.com/gamamhehe/Agentic.git
```

Layout:

```
Backend/
  C#/
    agents/
      Backend.agent.md
    instructions/
    skills/
    patterns/
    copilot-instructions.md
Frontend/
  Vue/
    agents/
      Frontend.agent.md
    instructions/
    skills/
    patterns/
    copilot-instructions.md
skills/
  BootstrapAgenticGuidance.skill.md    <- this file
README.md
```

---

## Step 1  Install agents to user space (one-time)

This step is done **once per developer machine**.
It places the agent orchestrators and the root entry point in VS Code user space
so they are available in every workspace.

### What to do

Ask the user which stacks they need  backend, frontend, or both  then execute the steps below.

### 1a. Clone to a temp location

Use the terminal in VS Code:

```bash
# Linux / macOS
TMP=$(mktemp -d) && git clone --depth 1 https://github.com/gamamhehe/Agentic.git "$TMP"
```

```powershell
# Windows
$tmp = Join-Path $env:TEMP "agentic-$(Get-Random)"
git clone --depth 1 https://github.com/gamamhehe/Agentic.git $tmp
```

### 1b. Copy the agent file(s) to user space

**Backend agent (C#):**

```bash
mkdir -p "$HOME/.github/Backend"
cp "$TMP/Backend/C#/agents/Backend.agent.md" "$HOME/.github/Backend/"
```

```powershell
New-Item "$env:USERPROFILE\.github\Backend" -ItemType Directory -Force | Out-Null
Copy-Item "$tmp\Backend\C#\agents\Backend.agent.md" "$env:USERPROFILE\.github\Backend\"
```

**Frontend agent (Vue):**

```bash
mkdir -p "$HOME/.github/Frontend"
cp "$TMP/Frontend/Vue/agents/Frontend.agent.md" "$HOME/.github/Frontend/"
```

```powershell
New-Item "$env:USERPROFILE\.github\Frontend" -ItemType Directory -Force | Out-Null
Copy-Item "$tmp\Frontend\Vue\agents\Frontend.agent.md" "$env:USERPROFILE\.github\Frontend\"
```

### 1c. Write the root copilot-instructions.md

Create `%USERPROFILE%\.github\copilot-instructions.md` (or `~/.github/copilot-instructions.md`)
with content matching the stacks installed:

**Both stacks:**

```markdown
# Copilot Instructions

## Backend (C#)
Use `Backend/Backend.agent.md` as the orchestrator for all backend tasks.
Stack-specific instructions, skills, and patterns are in `.github/Backend/C#/` inside the project repo.

## Frontend (Vue + Tailwind)
Use `Frontend/Frontend.agent.md` as the orchestrator for all frontend tasks.
Stack-specific instructions, skills, and patterns are in `.github/Frontend/Vue/` inside the project repo.
```

### 1d. Clean up

```bash
rm -rf "$TMP"
```

```powershell
Remove-Item $tmp -Recurse -Force
```

---

## Step 2  Pull stack guidance into a project (per project, on demand)

This step is run inside a specific project repo when the developer wants Copilot
to have full stack context for that workspace.

The user triggers this with a prompt like:

- *"Install the backend stack guidance into this project"*
- *"Pull the Vue guidance into this repo"*
- *"Set up Copilot guidance for this workspace"*

### What to do

1. Confirm which stack(s) to pull: `backend`, `frontend`, or `both`.
2. Check that `git` is available in the terminal.
3. Clone the Agentic repo to a temp location (same as Step 1a).
4. Copy the stack folders into the project's `.github/` directory:

**Backend (C#):**

```bash
DEST=".github/Backend/C#"
mkdir -p "$DEST"
for f in instructions skills patterns; do
  cp -r "$TMP/Backend/C#/$f" "$DEST/"
done
cp "$TMP/Backend/C#/copilot-instructions.md" "$DEST/"
```

```powershell
$dest = ".github\Backend\C#"
foreach ($f in @("instructions","skills","patterns")) {
    $s = Join-Path $tmp "Backend\C#\$f"
    $d = Join-Path $dest $f
    if (Test-Path $s) { New-Item $d -ItemType Directory -Force | Out-Null ; Copy-Item "$s\*" $d -Recurse -Force }
}
Copy-Item "$tmp\Backend\C#\copilot-instructions.md" $dest -Force
```

**Frontend (Vue):**

```bash
DEST=".github/Frontend/Vue"
mkdir -p "$DEST"
for f in instructions skills patterns; do
  cp -r "$TMP/Frontend/Vue/$f" "$DEST/"
done
cp "$TMP/Frontend/Vue/copilot-instructions.md" "$DEST/"
```

```powershell
$dest = ".github\Frontend\Vue"
foreach ($f in @("instructions","skills","patterns")) {
    $s = Join-Path $tmp "Frontend\Vue\$f"
    $d = Join-Path $dest $f
    if (Test-Path $s) { New-Item $d -ItemType Directory -Force | Out-Null ; Copy-Item "$s\*" $d -Recurse -Force }
}
Copy-Item "$tmp\Frontend\Vue\copilot-instructions.md" $dest -Force
```

5. Clean up the temp clone.
6. Confirm the result by listing `.github/` in the workspace.

---

## Wiring  how Copilot resolves guidance

```
User space ~/.github/copilot-instructions.md
  -> references Backend/Backend.agent.md   (orchestrator, always available)
  -> references Frontend/Frontend.agent.md (orchestrator, always available)

Project space {workspaceRoot}/.github/
  Backend/C#/
    instructions/   <- loaded by the agent when working on C# tasks
    skills/
    patterns/
  Frontend/Vue/
    instructions/   <- loaded by the agent when working on Vue tasks
    skills/
    patterns/
```

The agent files in user space are **always active**.
They look for stack guidance in the project `.github/` folder when executing a task.
If no project-level stack guidance is found, the agent will note the gap and ask the user to pull it.

---

## Expected result after full setup

**User space:**

```
~/.github/
  copilot-instructions.md
  Backend/
    Backend.agent.md
  Frontend/
    Frontend.agent.md
```

**Project space (per repo):**

```
{workspaceRoot}/
  .github/
    Backend/
      C#/
        copilot-instructions.md
        instructions/
        skills/
        patterns/
    Frontend/
      Vue/
        copilot-instructions.md
        instructions/
        skills/
        patterns/
```

---

## Verification

1. Open VS Code in any workspace.
2. Open Copilot Chat.
3. Ask: *"What guidance do you have loaded?"*

Copilot should mention the agent file(s) from user space.
If stack guidance has been pulled into the project, it should mention those too.

If Copilot does not pick up instructions:

- Confirm `~/.github/copilot-instructions.md` exists.
- Confirm VS Code setting `github.copilot.chat.codeGeneration.useInstructionFiles` is `true`.
- Confirm VS Code **1.93+** is installed.

---

## Updating guidance

To get the latest version of any tier:

- **Agents (user space):** re-run Step 1  re-copy the agent files.
- **Stack guidance (project space):** ask Copilot *"Update the backend stack guidance"* or re-run Step 2 for the relevant stack.
