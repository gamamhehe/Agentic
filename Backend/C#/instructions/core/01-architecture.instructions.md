---
name: Architecture-Instructions
description: Cross-layer architecture reference — project roles, dependencies, and boundary rules.
applyTo: "**"
---

# Architecture Instructions

## Layer Breakdown

| Project            | Role                                                                                                     |
| ------------------ | -------------------------------------------------------------------------------------------------------- |
| **Domain**         | Core business models, enums, exceptions, utilities. No dependencies on other layers.                     |
| **Application**    | Use-cases: CQRS commands/queries, DTOs, pipeline behaviors, interfaces. Depends only on Domain.          |
| **Infrastructure** | Persistence, caching, external adapters, observability, telemetry. Implements Application interfaces.    |
| **WebApi**         | Minimal API endpoints, middleware, DI bootstrapping, OpenAPI. Depends on Application and Infrastructure. |

## Dependency Rules

- Domain → no outward dependencies
- Application → depends only on Domain
- Infrastructure → depends on Application and Domain
- WebApi → depends on Application and Infrastructure
- Dependencies point inward toward business logic

## Boundary Rules

- Domain owns business rules and concepts
- Application coordinates use-cases and orchestration
- Infrastructure owns technical details and integrations
- WebApi owns HTTP transport concerns only
- Keep DTOs, EF Core mappings, HTTP models out of Domain
- Keep business logic out of endpoints and middleware

## Pattern File Index

| Concern                             | Pattern file                                |
| ----------------------------------- | ------------------------------------------- |
| Project layout                      | `patterns/structure.pattern.md`             |
| API endpoints / OpenAPI             | `patterns/api.pattern.md`                   |
| CQRS handlers / validation          | `patterns/application.pattern.md`           |
| Repositories, caching, DI, adapters | `patterns/infrastructure.pattern.md`        |
| EF Core audit / config              | `patterns/entity-framework-core.pattern.md` |
| Background jobs                     | `patterns/hangfire.pattern.md`              |
| Domain primitives                   | `patterns/domain.pattern.md`                |
| Telemetry / request logging         | `patterns/logging.pattern.md`               |
| Settings / options                  | `patterns/configuration.pattern.md`         |
| Tests                               | `patterns/testing.pattern.md`               |
