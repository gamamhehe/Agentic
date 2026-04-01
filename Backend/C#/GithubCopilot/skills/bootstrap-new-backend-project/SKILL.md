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
3. **Create SharedKernel project if it does not exist.**
   - Project name: `{SolutionName}.SharedKernel`
   - Target framework: same as other projects in the solution.
   - No dependencies on Domain, Application, Infrastructure, or WebApi.
   - Add minimum content:
     - `IUseCase` marker interface
     - `IUseCase<TRequest, TResponse>` with `ExecuteAsync`
     - `IUseCase<TRequest>` void variant with `ExecuteAsync`
   - Add project reference from Application to SharedKernel.
   - Add project reference from Infrastructure to SharedKernel.
   - Add project reference from WebApi to SharedKernel.
   - Verify build is green after wiring.
4. Call out missing architectural pieces such as test projects or execution conventions.
5. Treat project-wide use-case registration and validation flow as bootstrap work, not as a standalone feature skill.
6. Return a short follow-up checklist for team-specific governance decisions.

## SharedKernel Bootstrap Checklist

Use this checklist when creating or verifying a SharedKernel project:

- [ ] Project created with correct namespace: `{SolutionName}.SharedKernel`
- [ ] `IUseCase` marker interface exists
- [ ] `IUseCase<TRequest, TResponse>` contract exists with `Task<TResponse> ExecuteAsync(TRequest, CancellationToken)`
- [ ] `IUseCase<TRequest>` contract exists with `Task ExecuteAsync(TRequest, CancellationToken)`
- [ ] Application project references SharedKernel
- [ ] Infrastructure project references SharedKernel
- [ ] WebApi project references SharedKernel
- [ ] Solution builds green with no missing reference errors
- [ ] Optional: `IInteractor` added if team uses interactor/executor indirection

## Output

- installed guidance summary
- required next files or decisions
- architecture gaps to address next
- recommended follow-up setup work

## Escalate to / pair with

- pair with `build-use-case` when bootstrap leads directly into one feature implementation
- pair with `write-tests` when setup work needs verification coverage