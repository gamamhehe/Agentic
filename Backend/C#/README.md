# Backend Guidance for C# / .NET

Copilot-native backend guidance for C# and .NET repositories, optimized first for VS Code agent workflows and pull request review.

## What this pack contains

This folder is a reusable backend guidance pack built around the official Copilot artifact types:

- custom agent: `agents/backend-engineer.agent.md`
- repository baseline instructions: `copilot-instructions.md`
- path-specific instructions: `instructions/**/*.instructions.md`
- agent skills: `skills/<skill-name>/SKILL.md`
- reusable prompt files: `prompts/*.prompt.md`
- reference examples: `patterns/*.pattern.md`

Patterns are examples only. They help shape implementations, but they do not define policy.

## Recommended target layout in a real repository

```text
{workspaceRoot}/
  .github/
    agents/
      backend-engineer.agent.md
    instructions/
      core/
      cross-cutting/
      layers/
      project/
    skills/
      build-endpoint/
        SKILL.md
      review-pull-request/
        SKILL.md
      ...
    prompts/
      profile-current-project.prompt.md
      bootstrap-new-backend.prompt.md
      refactor-backend-feature.prompt.md
      review-backend-pr.prompt.md
      review-local-change.prompt.md
    patterns/
      *.pattern.md
    copilot-instructions.md
```

## Installation options

### Option 1: Workspace-level install for a team repository

Copy this prompt into Copilot Chat or another capable coding agent:

```text
Pull the backend C# / .NET GitHub Copilot guidance from https://github.com/gamamhehe/Agentic.git into this repository.

Create these folders in the workspace root if they do not exist:
- .github/agents/
- .github/instructions/
- .github/skills/
- .github/prompts/
- .github/patterns/

Copy:
- Backend/C#/agents/backend-engineer.agent.md -> .github/agents/backend-engineer.agent.md
- Backend/C#/copilot-instructions.md -> .github/copilot-instructions.md
- Backend/C#/instructions/* -> .github/instructions/   (preserve subfolders)
- Backend/C#/skills/* -> .github/skills/               (preserve subfolders)
- Backend/C#/prompts/* -> .github/prompts/
- Backend/C#/patterns/* -> .github/patterns/

Then show the resulting .github tree.
```

This is the best option when the repository should carry the same backend agent, skills, prompts, and review guidance for the whole team.

### Option 2: Install only the backend custom agent in VS Code user space

Use this when you want the backend agent available across multiple repositories, while each repository still supplies its own `.github` instructions and skills.

```text
Install the backend custom agent from https://github.com/gamamhehe/Agentic.git into my VS Code user-space custom agents location.

Copy:
- Backend/C#/agents/backend-engineer.agent.md

If a workspace already contains .github guidance, keep using the workspace instructions, skills, prompts, and patterns from that repository.
```

## How to use it

### Use the custom agent for day-to-day backend work

Choose `Backend-Engineer` in VS Code when you want Copilot to classify the task, load only the relevant instructions, and use the matching skill.

Good task examples:

- `Create an endpoint for GET /products`
- `Create a use case to place an order`
- `Add a Status property to the Order entity`
- `Implement IEmailSender with SendGrid`
- `Refactor the payment feature to follow clean architecture`
- `Review this backend change for architecture and testing issues`
- `Review this pull request for regressions and merge risk`

### Use prompt files for repeatable lead and engineer workflows

Prompt files give teams consistent entrypoints for recurring tasks:

- `prompts/profile-current-project.prompt.md`
- `prompts/bootstrap-new-backend.prompt.md`
- `prompts/refactor-backend-feature.prompt.md`
- `prompts/review-backend-pr.prompt.md`
- `prompts/review-local-change.prompt.md`

### Use project instructions to govern the agent

Keep project-specific decisions in:

- `instructions/project/domain-project.instructions.md`
- `instructions/project/team-standards.instructions.md`

Use the project templates when starting from scratch:

- `instructions/project/domain-project.instructions.template.md`
- `instructions/project/team-standards.instructions.template.md`
- `instructions/project/team-standards.example.instructions.md`

## Available backend skills

- `skills/profile-current-backend-project/SKILL.md`
- `skills/bootstrap-new-backend-project/SKILL.md`
- `skills/build-endpoint/SKILL.md`
- `skills/build-use-case/SKILL.md`
- `skills/wire-usecase-flow/SKILL.md`
- `skills/update-domain-model/SKILL.md`
- `skills/build-infrastructure-dependency/SKILL.md`
- `skills/configure-application-settings/SKILL.md`
- `skills/add-request-tracking/SKILL.md`
- `skills/write-tests/SKILL.md`
- `skills/refactor-backend-feature/SKILL.md`
- `skills/review-backend-change/SKILL.md`
- `skills/review-pull-request/SKILL.md`
- `skills/protect-backend-project/SKILL.md`

## Guidance hierarchy

Use backend guidance in this order:

1. instructions
2. skills
3. patterns

The custom agent is the orchestrator that decides what to load. Prompt files are user entrypoints for repeatable tasks.

## Verification

After installing into a repository:

1. Open VS Code in the target repo.
2. Open Copilot Chat.
3. Select `Backend-Engineer` if the custom agent is installed in the workspace.
4. Run one of the prompt files or ask a backend task in natural language.

Expected behavior:

- Copilot identifies the backend agent as the working surface.
- Copilot uses the relevant path-specific instructions instead of loading everything.
- Copilot can discover the skills under `.github/skills/<skill-name>/SKILL.md`.
- PR review tasks stay focused on correctness, merge risk, and test gaps.
