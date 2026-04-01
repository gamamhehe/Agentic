---
name: CSharp-Code-Style-Instructions
description: C# code conventions for maintainability, naming consistency, nullability safety, and project structure.
applyTo: "**/*.cs"
---

# C# Code Style Instructions

## Language Baseline

- Use modern C# syntax supported by the project target framework.
- Nullable reference types must remain enabled.
- Treat nullable warnings as design feedback, not noise.

## File and Type Structure

- File name must match the primary type name.
- Prefer file-scoped namespaces.
- Keep using directives minimal and remove unused imports.

## Class and Member Design

- Prefer constructor injection for dependencies.
- Keep classes focused on one responsibility.
- Make members as narrow as possible (`private` by default).
- Prefer immutable request/response models (`record` or `init` only setters).

## Async and Cancellation

- Use async all the way; avoid `.Result` and `.Wait()`.
- Methods doing asynchronous work must use `Async` suffix.
- Propagate `CancellationToken` through handlers, services, repositories, and external calls.

## Error and Result Handling

- Do not throw exceptions for expected business validation outcomes.
- Throw exceptions only for truly exceptional or infrastructure-failure scenarios.
- Return explicit result/error shapes used by the project patterns.

## Nullability and Defensive Checks

- Validate external inputs at boundaries (HTTP, queue, external API).
- Avoid null-forgiving operator (`!`) unless there is a proven invariant nearby.
- Prefer explicit guard clauses for required arguments.

## Data and Collections

- Use `IReadOnlyCollection<T>` or `IReadOnlyList<T>` for read-only outputs.
- Avoid exposing mutable collections from domain or application models.
- Use `var` when the right-hand side type is obvious; otherwise prefer explicit type.

## Logging and Observability

- Use structured logging with named placeholders.
- Never log secrets, tokens, raw credentials, or full sensitive payloads.
- Log business-significant state transitions and failure context.

## Forbidden Shortcuts

- No business rules inside controllers/endpoints or middleware.
- No direct Infrastructure references from Domain or Application.
- No swallowing exceptions without adding context and preserving diagnostics.