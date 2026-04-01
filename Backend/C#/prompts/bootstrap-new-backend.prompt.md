---
description: Bootstrap GitHub Copilot guidance for a new C# and .NET backend repository.
agent: agent
---

Use `@Backend-Engineer` if it is available.

Set up the backend Copilot guidance pack for this repository.

Tasks:

1. Install the backend custom agent, repository-wide instructions, path-specific instructions, skills, prompts, and patterns into the repo's `.github` structure.
2. Keep `copilot-instructions.md` concise and use project instructions for local domain and team decisions.
3. Copy the project instruction templates that still need repository-specific decisions.
4. Point out any missing architectural pieces such as SharedKernel, test projects, or standard layer projects.

Return:

1. `Files installed`
2. `Files that need team decisions`
3. `Architecture gaps to address next`
