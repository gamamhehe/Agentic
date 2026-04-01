---
name: Testing-Instructions
description: Standards for test structure, naming, isolation, and assertion style.
applyTo: "tests/**"
---

# Testing Instructions

See `patterns/testing.pattern.md` for code examples.

## Project Structure

| Project                           | Purpose                                                            |
| --------------------------------- | ------------------------------------------------------------------ |
| `{ProjectName}.Domain.Tests`      | Unit tests for domain models, value objects, business rules        |
| `{ProjectName}.Application.Tests` | Unit tests for UseCases, validators, execution flow — mocked interfaces |
| `{ProjectName}.IntegrationTests`  | End-to-end tests against real or in-memory infrastructure          |

## Unit Test Rules

- One test class per subject
- Class naming: `{SubjectUnderTest}Tests`
- Method naming: `{Method}_When{Condition}_Should{ExpectedOutcome}`
- **NSubstitute** for mocking
- **FluentAssertions** for assertions
- Never instantiate Infrastructure classes in Application.Tests

## Application Test Rules

- Mock all interfaces from `Application/Common/Interfaces/`
- Test UseCases in isolation — mock repositories/services, verify returned result shape
- Test validators using `TestValidate()` from `FluentValidation.TestHelper`

## Integration Test Rules

- `WebApplicationFactory<T>` for full API tests
- Dedicated test database or in-memory equivalent
- Reset state between runs — no shared mutable state
- Full slice: HTTP request → UseCase execution flow → infrastructure

## General Rules

- Deterministic — no `DateTime.Now` without abstraction, no random data
- Prefer `[Theory]` + `[InlineData]` for data-driven scenarios
- Minimal test setup — use builders or factories for complex objects
