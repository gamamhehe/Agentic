---
name: dotnet-backend-rules
description: Foundational rulebook for C# and .NET backend repositories. Use for any non-trivial .NET backend implementation, refactor, profiling, review, or bootstrap task so Codex can apply the same architecture, layer, testing, review, and reference-pattern guidance that the GitHub Copilot pack provides.
---

# Dotnet Backend Rules

Load this skill for any non-trivial backend work in a repository that contains `.sln`, `*.csproj`, `Directory.Build.props`, `Directory.Packages.props`, or `global.json`.

This skill is the Codex equivalent of the GitHub Copilot instruction pack. It consolidates the Copilot baseline, layer rules, cross-cutting review rules, and reference patterns into one reusable skill.

## When to use

Use this skill before implementation, refactor, profiling, review, or bootstrap work in a C# and .NET backend repository.

## What this skill owns

- always-on backend architecture rules
- layer boundaries and dependency direction
- naming and C# code-style expectations
- configuration, testing, review-gate, and PR-review rules
- reference code patterns for API, application, domain, infrastructure, configuration, logging, EF Core, Hangfire, structure, and tests

## What stays outside this skill

- project-specific business language and invariants in repository-root `domain-project.instructions.md`
- task-specific execution details in focused skills such as `build-endpoint`, `build-use-case`, or `review-pull-request`
- repository-specific implementation facts discovered by reading the target codebase

## Required reading order

1. Read this `SKILL.md`.
2. If present, read repository-root `domain-project.instructions.md` for project business rules.
3. Read only the relevant bundled reference files for the touched concern.
4. Load one focused task skill for the actual job.
5. Use bundled pattern references as examples, not policy.

## Reference map

### Core rules

- `references/core/01-architecture.instructions.md`
- `references/core/02-naming.instructions.md`
- `references/core/03-csharp-code-style.instructions.md`

Read these for every non-trivial .NET backend task.

### Cross-cutting rules

- `references/cross-cutting/20-configuration.instructions.md`
- `references/cross-cutting/21-testing.instructions.md`
- `references/cross-cutting/22-review-gates.instructions.md`
- `references/cross-cutting/23-pr-review.instructions.md`

Read the relevant files when config, tests, merge safety, rollout, auth, data safety, or PR review are in scope.

### Layer rules

- `references/layers/10-domain.instructions.md`
- `references/layers/11-application.instructions.md`
- `references/layers/12-infrastructure.instructions.md`
- `references/layers/13-webapi.instructions.md`

Read only the touched layer plus any directly adjacent layer.

### Project guidance models

- `references/project/team-standards.instructions.md`
- `references/project/team-standards.example.instructions.md`
- `references/project/team-standards.instructions.template.md`
- `references/project/domain-project.instructions.template.md`

Use these as models when the target repository is missing local governance files.

### Reference code patterns

- `references/patterns/structure.pattern.md`
- `references/patterns/api.pattern.md`
- `references/patterns/application.pattern.md`
- `references/patterns/domain.pattern.md`
- `references/patterns/infrastructure.pattern.md`
- `references/patterns/entity-framework-core.pattern.md`
- `references/patterns/hangfire.pattern.md`
- `references/patterns/logging.pattern.md`
- `references/patterns/configuration.pattern.md`
- `references/patterns/testing.pattern.md`

Use these as concrete examples after the rules are clear. Patterns never override architecture or review rules.

## Operating rules

- Preserve clean layer boundaries. Domain and SharedKernel stay free of Infrastructure and transport concerns.
- Keep business logic out of endpoints, middleware, infrastructure adapters, and configuration glue.
- Prefer explicit names, realistic shapes, and predictable behavior over hidden magic.
- Preserve behavior unless the request explicitly changes behavior.
- Treat nullability, cancellation, validation, configuration, logging, observability, and test coverage as design responsibilities.
- Require at least one meaningful happy-path test for changed behavior and add failure, validation, cancellation, auth, contract, or integration coverage when risk justifies it.
- Block approval when auth, migrations, contracts, integrations, jobs, or operational safety are under-specified.

## Pair with

- `profile-current-backend-project` to understand the current repo before work begins
- `bootstrap-new-backend-project` to install or repair backend guidance and execution conventions
- `update-domain-model` for business-rule changes
- `build-use-case` for orchestration changes
- `build-endpoint` for HTTP surface changes
- `build-infrastructure-dependency` for persistence, integrations, jobs, config, or observability work
- `write-tests` for focused coverage work
- `refactor-backend-feature` for behavior-preserving cleanup
- `review-backend-change` or `review-pull-request` for review work

## Output expectations

For implementation or refactor work, prefer:

- short plan
- design notes
- change summary
- tests or verification notes
- guidance gaps when present

For profiling work, prefer:

- architecture snapshot
- conventions detected
- drift or risk areas
- missing governance decisions
- recommended next steps

For review work, prefer:

- verdict first
- findings ordered by severity
- test gaps
- guidance gaps
- short summary only after findings
