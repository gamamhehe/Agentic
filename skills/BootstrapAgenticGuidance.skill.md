# Bootstrap Agentic Guidance

## Purpose

This file is a **prompt script**.
Copy the relevant section below and paste it into any AI chat (GitHub Copilot, ChatGPT, Claude, etc.).
The AI will execute every step: clone the repo, copy the files, and clean up.

---

## Prompt  Install agents to user space (run once per machine)

> Copy everything inside the block and paste it into your AI chat.

---

**Paste this prompt:**

```
I want to set up AI guidance from https://github.com/gamamhehe/Agentic.git into my VS Code user space so it applies to all my workspaces.

Please do the following steps for me:

1. Clone the repo with a shallow clone (--depth 1) into a temporary directory.

2. Detect my OS:
   - Windows: user space is %USERPROFILE%\.github\
   - Linux / macOS: user space is ~/.github/

3. Create the following folders in user space if they do not exist:
   - Backend/
   - Frontend/

4. Copy these files from the cloned repo to user space:
   - Backend/C#/agents/Backend.agent.md  ->  {userSpace}/Backend/Backend.agent.md
   - Frontend/Vue/agents/Frontend.agent.md  ->  {userSpace}/Frontend/Frontend.agent.md

5. Create the file {userSpace}/copilot-instructions.md with this exact content:

# Copilot Instructions

## Backend (C#)
Use `Backend/Backend.agent.md` as the orchestrator for all backend tasks.
Stack-specific instructions, skills, and patterns live in `.github/Backend/C#/` inside each project repo.

## Frontend (Vue + Tailwind)
Use `Frontend/Frontend.agent.md` as the orchestrator for all frontend tasks.
Stack-specific instructions, skills, and patterns live in `.github/Frontend/Vue/` inside each project repo.

6. Delete the temporary clone directory completely.

7. Show me the final file tree under my user space .github/ folder so I can confirm everything is in place.
```

---

## Prompt  Pull backend stack guidance into the current project

> Open the project in VS Code, open AI chat, and paste this prompt.

---

**Paste this prompt:**

```
I want to pull the C# / .NET stack guidance from https://github.com/gamamhehe/Agentic.git into this project so GitHub Copilot has full context for this workspace.

Please do the following steps for me:

1. Clone the repo with a shallow clone (--depth 1) into a temporary directory.

2. Create the folder .github/Backend/C#/ in the current workspace root if it does not exist.

3. Copy these folders from the cloned repo into .github/Backend/C#/:
   - Backend/C#/instructions/
   - Backend/C#/skills/
   - Backend/C#/patterns/

4. Copy the file Backend/C#/copilot-instructions.md into .github/Backend/C#/copilot-instructions.md

5. Delete the temporary clone directory completely.

6. Show me the final file tree under .github/ so I can confirm everything is in place.
```

---

## Prompt  Pull frontend stack guidance into the current project

> Open the project in VS Code, open AI chat, and paste this prompt.

---

**Paste this prompt:**

```
I want to pull the Vue + Tailwind stack guidance from https://github.com/gamamhehe/Agentic.git into this project so GitHub Copilot has full context for this workspace.

Please do the following steps for me:

1. Clone the repo with a shallow clone (--depth 1) into a temporary directory.

2. Create the folder .github/Frontend/Vue/ in the current workspace root if it does not exist.

3. Copy these folders from the cloned repo into .github/Frontend/Vue/:
   - Frontend/Vue/instructions/
   - Frontend/Vue/skills/
   - Frontend/Vue/patterns/

4. Copy the file Frontend/Vue/copilot-instructions.md into .github/Frontend/Vue/copilot-instructions.md

5. Delete the temporary clone directory completely.

6. Show me the final file tree under .github/ so I can confirm everything is in place.
```

---

## Prompt  Pull both stacks into the current project

> Use this when a project uses both C# backend and Vue frontend.

---

**Paste this prompt:**

```
I want to pull both the C# backend and Vue + Tailwind frontend stack guidance from https://github.com/gamamhehe/Agentic.git into this project.

Please do the following steps for me:

1. Clone the repo with a shallow clone (--depth 1) into a temporary directory.

2. Backend  create .github/Backend/C#/ if it does not exist, then copy:
   - Backend/C#/instructions/  ->  .github/Backend/C#/instructions/
   - Backend/C#/skills/        ->  .github/Backend/C#/skills/
   - Backend/C#/patterns/      ->  .github/Backend/C#/patterns/
   - Backend/C#/copilot-instructions.md  ->  .github/Backend/C#/copilot-instructions.md

3. Frontend  create .github/Frontend/Vue/ if it does not exist, then copy:
   - Frontend/Vue/instructions/  ->  .github/Frontend/Vue/instructions/
   - Frontend/Vue/skills/        ->  .github/Frontend/Vue/skills/
   - Frontend/Vue/patterns/      ->  .github/Frontend/Vue/patterns/
   - Frontend/Vue/copilot-instructions.md  ->  .github/Frontend/Vue/copilot-instructions.md

4. Delete the temporary clone directory completely.

5. Show me the final file tree under .github/ so I can confirm everything is in place.
```

---

## Prompt  Update guidance (re-pull latest)

> Use this to refresh any previously installed guidance to the latest version.

---

**Paste this prompt:**

```
I want to update my Agentic guidance to the latest version from https://github.com/gamamhehe/Agentic.git.

Please ask me first:
- Do you want to update user space agents, project stack guidance, or both?
- Which stack(s)? Backend (C#), Frontend (Vue), or both?

Then follow the same steps as the original install prompts above (clone, copy, delete temp clone), overwriting any existing files.
```

---

## Expected result after full setup

**User space (once per machine):**

```
~/.github/                          <- %USERPROFILE%\.github\ on Windows
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

## Verify

After running any prompt above, ask the AI:

```
Did everything complete successfully? Show me the .github/ file tree.
```

Then open VS Code Copilot Chat and ask:

```
What guidance do you have loaded?
```

Copilot should mention `Backend.agent.md` and/or `Frontend.agent.md`.

If it does not:
- Confirm `~/.github/copilot-instructions.md` exists.
- Confirm VS Code setting `github.copilot.chat.codeGeneration.useInstructionFiles` is `true`.
- Confirm VS Code **1.93+** is installed.
