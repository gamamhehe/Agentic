# Backend Guidance C# / .NET

AI guidance for C# / .NET projects using GitHub Copilot.

Stack: **C#**, **.NET**, **Entity Framework Core**

---

## What is this?

This folder provides structured guidance that GitHub Copilot uses to assist with backend tasks.
It follows a **two-tier model**:

| Tier              | Content                                          | Where it lives                                                         | When                         |
| ----------------- | ------------------------------------------------ | ---------------------------------------------------------------------- | ---------------------------- |
| **User space**    | `backend-engineer.agent.md` (main backend agent) | `~/.github/agents/`                                                    | Installed once per machine   |
| **Project space** | `instructions/`, `skills/`, `patterns/`          | `{repo}/.github/instructions/`, `.github/skills/`, `.github/patterns/` | Pulled per project on demand |

---

## Tier 1 — Install the agent to user space (one-time)

This makes the Backend agent available in **every VS Code workspace** on this machine.

Copy the prompt below and paste it into any AI chat (Copilot, ChatGPT, Claude, etc.).
The AI will clone the repo, copy the agent file, and clean up.

```
I want to set up AI guidance from https://github.com/gamamhehe/Agentic.git into my VS Code user space so it applies to all my workspaces.

Please do the following steps for me:

1. Clone the repo with a shallow clone (--depth 1) into a temporary directory.

2. Detect my OS:
   - Windows: user space is %USERPROFILE%\.github\
   - Linux / macOS: user space is ~/.github/

3. Create the following folder in user space if it does not exist:
   - agents/

4. Copy these files from the cloned repo to user space:
   - Backend/C#/agents/backend-engineer.agent.md  ->  {userSpace}/agents/Backend-Engineer.agent.md
   - Frontend/Vue/agents/Frontend.agent.md         ->  {userSpace}/agents/Frontend.agent.md

5. Delete the temporary clone directory completely.

6. Show me the final file tree under my user space .github/ folder so I can confirm everything is in place.
```

### Result in user space

```
~/.github/
  agents/
    Backend-Engineer.agent.md
    Frontend.agent.md
```

---

## Tier 2 — Pull stack guidance into a project (per repo)

Run this inside the specific project where you want full C# context.
Copy the prompt below and paste it into any AI chat.

```
I want to pull the C# / .NET stack guidance from https://github.com/gamamhehe/Agentic.git into this project so GitHub Copilot has full context for this workspace.

Please do the following steps for me:

1. Clone the repo with a shallow clone (--depth 1) into a temporary directory.

2. Create the following folders in the current workspace root if they do not exist:
   - .github/instructions/
   - .github/skills/
   - .github/patterns/

3. Copy these folders and files from the cloned repo:
   - Backend/C#/instructions/*   ->  .github/instructions/   (preserve subfolders)
   - Backend/C#/skills/*         ->  .github/skills/
   - Backend/C#/patterns/*       ->  .github/patterns/

4. Copy the file Backend/C#/copilot-instructions.md into .github/copilot-instructions.md as a minimal project entry file.

5. Delete the temporary clone directory completely.

6. Show me the final file tree under .github/ so I can confirm everything is in place.
```

### Result in project space

```
{workspaceRoot}/
  .github/
    copilot-instructions.md
    instructions/
      core/
        01-architecture.instructions.md
        02-naming.instructions.md
      layers/
        10-domain.instructions.md
        11-application.instructions.md
        12-infrastructure.instructions.md
        13-webapi.instructions.md
      cross-cutting/
        20-configuration.instructions.md
        21-testing.instructions.md
      project/
        domain-project.instructions.template.md
    skills/
      add-request-tracking.skill.md
      build-endpoint.skill.md
      build-infrastructure-dependency.skill.md
      build-use-case.skill.md
      configure-application-settings.skill.md
      refactor-backend-feature.skill.md
      review-backend-change.skill.md
      update-domain-model.skill.md
      write-tests.skill.md
    patterns/
      api.pattern.md
      application.pattern.md
      configuration.pattern.md
      domain.pattern.md
      entity-framework-core.pattern.md
      hangfire.pattern.md
      infrastructure.pattern.md
      logging.pattern.md
      structure.pattern.md
      testing.pattern.md
```

---

## How to use

Once the agent (Tier 1) is in user space, Copilot is ready for backend tasks in any workspace.
Once the stack guidance (Tier 2) is pulled into a project, Copilot has full context for that repo.

Use natural language in Copilot Chat:

| Task                      | What to say                                                   |
| ------------------------- | ------------------------------------------------------------- |
| Create a new API endpoint | _"Create an endpoint for GET /products"_                      |
| Add a use case / command  | _"Create a use case to place an order"_                       |
| Update the domain model   | _"Add a Status property to the Order entity"_                 |
| Implement infrastructure  | _"Implement the IEmailSender with SendGrid"_                  |
| Review a change           | _"Review this change for architecture issues"_                |
| Write tests               | _"Write tests for the CreateOrderUseCase"_                    |
| Refactor a feature        | _"Refactor the payment feature to follow clean architecture"_ |

`.github/copilot-instructions.md` is only a lightweight project entry file.
The real backend behavior lives in `backend-engineer.agent.md`, which loads the relevant instructions, skills, and patterns for the task.

---

## Customise for your project

Keep `.github/copilot-instructions.md` minimal.

Use these project files to tailor behavior:

- optional project-specific domain guidance file if your repo defines one

---

## Update guidance

Re-copy the relevant prompt above and paste it into AI chat again. It will overwrite with the latest version.

---

## Verify

1. Open VS Code in any workspace.
2. Open Copilot Chat.
3. Ask: _"What guidance do you have loaded?"_

Copilot should mention `backend-engineer.agent.md`.
If stack guidance is pulled into the project, it should also mention the relevant instruction, skill, and pattern files for the task.

If it does not:

- Confirm `~/.github/agents/Backend-Engineer.agent.md` exists.
- Confirm `{workspaceRoot}/.github/copilot-instructions.md` exists.
- Confirm VS Code setting `github.copilot.chat.codeGeneration.useInstructionFiles` is `true`.
- Confirm VS Code **1.93+** is installed.
  | All skills | Same names (kebab-case) |
  | All patterns | Same names (kebab-case with `.pattern.md` suffix) |
