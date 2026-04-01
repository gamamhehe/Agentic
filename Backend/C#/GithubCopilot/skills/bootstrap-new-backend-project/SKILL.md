---
name: bootstrap-new-backend-project
description: Set up backend guidance and project-wide engineering conventions for a new C# and .NET repository.
---

# Bootstrap New Backend Project

## When to use

Use this skill when a new backend repository needs guidance, baseline architecture setup, or project-wide execution conventions.

## Primary boundary

Lifecycle boundary: project bootstrap and project-wide setup.

## Out of scope

- implementing one feature endpoint or one use case
- detailed infrastructure adapter work for a single integration
- local code review of an existing patch

## Typical inputs

- repository root
- solution or project naming choice
- whether Domain, Application, Infrastructure, WebApi, and SharedKernel already exist
- team-specific governance preferences when available

## Workflow

1. Install the backend guidance structure needed for the chosen tool surface.
2. Check whether the repository has the expected layer and test project layout.
3. Call out missing architectural pieces such as SharedKernel, test projects, or execution conventions.
4. Treat project-wide use-case registration and validation flow as bootstrap work, not as a standalone feature skill.
5. Return a short follow-up checklist for team-specific governance decisions.

## Output

- installed guidance summary
- required next files or decisions
- architecture gaps to address next
- recommended follow-up setup work

## Escalate to / pair with

- pair with `build-use-case` when bootstrap leads directly into one feature implementation
- pair with `write-tests` when setup work needs verification coverage
