---
name: Architecture-Instructions
description: Cross-layer architecture reference — project roles, dependencies, and boundary rules.
applyTo: "**"
---

# Architecture Instructions
## Layer Breakdown

| Project | Required | Role | Bootstrap notes |
| --- | --- | --- | --- |
| **SharedKernel** | Yes | Cross-cutting contracts and abstractions shared across layers, such as `IUseCase` and `IInteractor`. No infrastructure or framework dependencies. | Must exist before any UseCase work begins. Contains runtime-safe shared contracts only. |
| **Domain** | Yes | Core business models, enums, exceptions, and utilities. No dependencies on other layers. | Created at solution initialization. Must remain independent of other layers. |
| **Application** | Yes | UseCase implementations, request/response models, validators, and interfaces. Depends on Domain and SharedKernel. | Created before feature implementation. Depends only on Domain and SharedKernel. |
| **Infrastructure** | Yes | Persistence, caching, external adapters, observability, and telemetry. Implements Application interfaces and SharedKernel runtime contracts. | Must implement Application abstractions and contain technical integrations only. |
| **WebApi** | Yes | Minimal API endpoints, middleware, dependency injection bootstrapping, and OpenAPI setup. Depends on Application, Infrastructure, and SharedKernel runtime contracts. | Hosts the HTTP surface and composition root for the backend solution. |


### SharedKernel Minimum Content

A new SharedKernel project must contain at minimum:

- IUseCase marker interface
- IUseCase<TRequest, TResponse> generic contract with ExecuteAsync
- IUseCase<TRequest> void/unit variant with ExecuteAsync
- Optional: IInteractor when the team uses the interactor/executor indirection pattern

If SharedKernel does not exist when UseCase work is requested, create the project before implementing the first UseCase.
## Dependency Rules

- SharedKernel → no outward dependencies
- Domain → no outward dependencies
- Application → depends on Domain and SharedKernel
- Infrastructure → depends on Application, Domain, and SharedKernel
- WebApi → depends on Application, Infrastructure, and SharedKernel
- Dependencies point inward toward business logic

## Boundary Rules

- Domain owns business rules and concepts
- SharedKernel owns cross-cutting contracts (`IUseCase`, `IInteractor`) shared across projects
- Application coordinates use-cases and orchestration
- Infrastructure owns technical details and integrations
- WebApi owns HTTP transport concerns only
- Keep DTOs, EF Core mappings, HTTP models out of Domain
- Keep business logic out of endpoints and middleware
- Keep `IUseCase` and other shared execution contracts out of Application project and place them in SharedKernel

## Pattern File Index

| Concern                             | Pattern file                                |
| ----------------------------------- | ------------------------------------------- |
| Project layout                      | `patterns/structure.pattern.md`             |
| API endpoints / OpenAPI             | `patterns/api.pattern.md`                   |
| UseCase shape / validation / DI     | `patterns/application.pattern.md`           |
| Repositories, caching, DI, adapters | `patterns/infrastructure.pattern.md`        |
| EF Core audit / config              | `patterns/entity-framework-core.pattern.md` |
| Background jobs                     | `patterns/hangfire.pattern.md`              |
| Domain primitives                   | `patterns/domain.pattern.md`                |
| Telemetry / request logging         | `patterns/logging.pattern.md`               |
| Settings / options                  | `patterns/configuration.pattern.md`         |
| Tests                               | `patterns/testing.pattern.md`               |
