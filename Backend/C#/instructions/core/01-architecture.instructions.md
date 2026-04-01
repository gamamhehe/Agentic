---
name: Architecture-Instructions
description: Cross-layer architecture reference — project roles, dependencies, and boundary rules.
applyTo: "**"
---

# Architecture Instructions

## Layer Breakdown

| Project            | Role                                                                                                     |
| ------------------ | -------------------------------------------------------------------------------------------------------- |
| **SharedKernel**   | Cross-cutting contracts and abstractions shared across layers (e.g., `IUseCase`, `IInteractor`). No infrastructure/framework dependencies. |
| **Domain**         | Core business models, enums, exceptions, utilities. No dependencies on other layers.                     |
| **Application**    | UseCase implementations, request/response models, validators, interfaces. Depends on Domain and SharedKernel. |
| **Infrastructure** | Persistence, caching, external adapters, observability, telemetry. Implements Application interfaces and SharedKernel runtime contracts. |
| **WebApi**         | Minimal API endpoints, middleware, DI bootstrapping, OpenAPI. Depends on Application, Infrastructure, and SharedKernel contracts used at runtime. |

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
