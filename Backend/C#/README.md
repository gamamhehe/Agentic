# Backend Guidance C# / .NET

AI guidance for C# / .NET projects using GitHub Copilot.

Stack: **C#**, **.NET**, **Entity Framework Core**

---

## What is this?

This folder provides structured guidance that GitHub Copilot uses to assist with backend tasks.
It follows a **two-tier model**:

| Tier              | Content                                 | Where it lives                                                         | When                         |
| ----------------- | --------------------------------------- | ---------------------------------------------------------------------- | ---------------------------- |
| **User space**    | `Backend.agent.md` (orchestrator)       | `~/.github/agents/`                                                    | Installed once per machine   |
| **Project space** | `instructions/`, `skills/`, `patterns/` | `{repo}/.github/instructions/`, `.github/skills/`, `.github/patterns/` | Pulled per project on demand |

---

## Tier 1 Install the agent to user space (one-time)

This makes the Backend agent available in **every VS Code workspace** on this machine.

Copy the prompt below and paste it into any AI chat (Copilot, ChatGPT, Claude, etc.).
The AI will clone the repo, copy the agent file, write the entry point, and clean up.

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
   - Backend/C#/agents/Backend.agent.md    ->  {userSpace}/agents/Backend.agent.md
   - Frontend/Vue/agents/Frontend.agent.md  ->  {userSpace}/agents/Frontend.agent.md

5. Delete the temporary clone directory completely.

6. Show me the final file tree under my user space .github/ folder so I can confirm everything is in place.
```

### Result in user space

```
~/.github/
  copilot-instructions.md
  agents/
    Backend.agent.md
    Frontend.agent.md
```

---

## Tier 2 Pull stack guidance into a project (per repo)

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

3. Copy these files from the cloned repo:
   - Backend/C#/instructions/*           ->  .github/instructions/
   - Backend/C#/skills/*                 ->  .github/skills/
   - Backend/C#/patterns/*               ->  .github/patterns/

4. Copy the file Backend/C#/copilot-instructions.md into .github/copilot-instructions.md

5. Delete the temporary clone directory completely.

6. Show me the final file tree under .github/ so I can confirm everything is in place.
```

### Result in project space

```
{workspaceRoot}/
  .github/
    copilot-instructions.md
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

Copilot loads `Backend.agent.md`, selects the relevant skill, and applies the instructions and patterns.

---

## Customise for your project

After pulling stack guidance, open `.github/copilot-instructions.md` and replace the placeholders:

```markdown
- Language/runtime: .NET `{DotNetVersion}` -> e.g. .NET 9
- Database: `{Database}` -> e.g. Postgres
- Background jobs: `{JobRunner}` -> e.g. Hangfire
```

For project-specific domain rules, edit `.github/instructions/Domain.Project.Instructions.md`.

---

## Update guidance

Re-copy the relevant prompt above and paste it into AI chat again. It will overwrite with the latest version.

---

## Verify

1. Open VS Code in any workspace.
2. Open Copilot Chat.
3. Ask: _"What guidance do you have loaded?"_

Copilot should mention `Backend.agent.md`.
If stack guidance is pulled into the project, it should mention the instruction files too.

If it does not:

- Confirm `~/.github/copilot-instructions.md` exists.
- Confirm VS Code setting `github.copilot.chat.codeGeneration.useInstructionFiles` is `true`.
- Confirm VS Code **1.93+** is installed.
