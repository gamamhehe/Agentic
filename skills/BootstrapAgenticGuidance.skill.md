# Bootstrap Agentic Guidance Skill

## When to use

Use this skill when the user wants to set up or refresh the AI guidance configuration
(agents, instructions, skills, patterns) in a target project or in the VS Code user-level
`.github` directory.

Typical trigger phrases:

- "set up the AI guidance"
- "install the Agentic config"
- "bootstrap Copilot instructions"
- "download and extract the Agentic repo"
- "configure AI guidance for this project"

---

## What this skill does

Clones or updates the repository:

```
https://github.com/gamamhehe/Agentic.git
```

Then copies the AI guidance files into the correct destination so that
GitHub Copilot picks them up automatically.

---

## Destination paths

| Target                                                     | Path                                                             |
| ---------------------------------------------------------- | ---------------------------------------------------------------- |
| **VS Code user-level** (global, applies to all workspaces) | `%USERPROFILE%\.github\` (Windows) or `~/.github/` (Linux/macOS) |
| **Project-level** (applies only to the open workspace)     | `{workspaceRoot}\.github\`                                       |

The VS Code user-level path is read by GitHub Copilot as the global instruction source.
Place files there when the guidance should apply across **all projects**.
Place files in the project root `.github\` when the guidance is **project-specific**.

---

## Inputs

Before running, confirm with the user:

- **Destination**: user-level (`~/.github/`) or project-level (`{workspaceRoot}/.github/`)?
- **Mode**: fresh clone or update an existing copy?
- **Overwrite policy**: overwrite existing files, skip, or merge?

Default to **project-level** + **overwrite** if not specified.

---

## Steps

### 1. Check prerequisites

Verify `git` is available:

```powershell
git --version
```

If `git` is not found, instruct the user to install Git from https://git-scm.com and retry.

### 2. Resolve the destination directory

**User-level (Windows):**

```powershell
$dest = "$env:USERPROFILE\.github"
```

**User-level (Linux / macOS):**

```bash
dest="$HOME/.github"
```

**Project-level:**
Use the workspace root folder reported by the IDE.

### 3. Clone or update the repo into a temp location

```powershell
$tmp = Join-Path $env:TEMP "agentic-guidance-$(Get-Random)"
git clone --depth 1 https://github.com/gamamhehe/Agentic.git $tmp
```

A shallow clone (`--depth 1`) is used to keep it fast.

### 4. Copy guidance files to the destination

Copy only the AI guidance folders — do **not** copy `.git`, `README.md`, or project-specific files
unless the user explicitly requests them.

```powershell
$folders = @("agents", "instructions", "skills", "patterns")

foreach ($folder in $folders) {
    $src = Join-Path $tmp $folder
    $dst = Join-Path $dest $folder

    if (Test-Path $src) {
        if (-not (Test-Path $dst)) {
            New-Item -ItemType Directory -Path $dst | Out-Null
        }
        Copy-Item -Path "$src\*" -Destination $dst -Recurse -Force
    }
}
```

Also copy `copilot-instructions.md` to the destination root:

```powershell
$ciSrc = Join-Path $tmp "copilot-instructions.md"
if (Test-Path $ciSrc) {
    Copy-Item -Path $ciSrc -Destination $dest -Force
}
```

### 5. Clean up the temp clone

```powershell
Remove-Item -Path $tmp -Recurse -Force
```

### 6. Confirm the result

List the installed files so the user can verify:

```powershell
Get-ChildItem -Path $dest -Recurse | Select-Object FullName
```

---

## Output

After the skill completes, the following structure should exist at the destination:

```
{dest}/
  copilot-instructions.md        <- Copilot global instructions entry point
  agents/
    Backend.agent.md
  instructions/
    Application.instructions.md
    Architecture.instructions.md
    Domain.instructions.md
    Domain.Project.Instructions.md
    Infrastructure.instructions.md
    Naming.instructions.md
    Settings.instructions.md
    Testing.instructions.md
    WebApi.instructions.md
  skills/
    AddRequestTracking.skill.md
    ConfigureApplicationSettings.skill.md
    CreateEndpoint.skill.md
    CreateUseCase.skill.md
    ImplementInfrastructureDependency.skill.md
    RefactorBackendFeature.skill.md
    ReviewBackendChange.skill.md
    UpdateDomainModel.skill.md
    WriteTests.skill.md
    BootstrapAgenticGuidance.skill.md
  patterns/
    ApiPatterns.md
    ApplicationPatterns.md
    CodePatterns.md
    EntityFrameworkCorePatterns.md
    InfrastructurePatterns.md
    LogPatterns.md
    SettingsPatterns.md
    StructurePatterns.md
    TestingPatterns.md
```

---

## Verification

After installation, ask the user to:

1. Open VS Code.
2. Open any workspace.
3. Start a GitHub Copilot Chat session.
4. Ask: _"What guidance do you have loaded?"_

Copilot should reference the `copilot-instructions.md` and the `agents/Backend.agent.md` content.

If Copilot does not pick up the instructions, check:

- The `copilot-instructions.md` file is at `~/.github/copilot-instructions.md`
- VS Code setting `github.copilot.chat.codeGeneration.useInstructionFiles` is set to `true`

---

## Notes

- The VS Code user-level `.github` folder is supported from VS Code 1.93+.
- Project-level `.github/copilot-instructions.md` always takes precedence over user-level.
- After updating files, no VS Code restart is needed — Copilot reads the files on each request.
- To update guidance in the future, re-run this skill. The `--depth 1` clone always pulls the latest `main` branch.
