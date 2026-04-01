---
name: Testing-Instructions
description: Standards for test structure, naming, isolation, and assertion style.
applyTo: "tests/**"
---

# Testing Instructions

See `patterns/testing.pattern.md` for code examples.

## Project Structure

| Project | Purpose |
| --- | --- |
| `{ProjectName}.Domain.Tests` | Unit tests for domain models, value objects, and business rules |
| `{ProjectName}.Application.Tests` | Unit tests for use cases, validators, and execution flow with mocked interfaces |
| `{ProjectName}.IntegrationTests` | End-to-end tests against real or in-memory infrastructure |

## Unit Test Rules

- One test class per subject
- Class naming: `{SubjectUnderTest}Tests`
- Method naming: `{Method}_When{Condition}_Should{ExpectedOutcome}`
- Use **NSubstitute** for mocking
- Use **FluentAssertions** for assertions
- Never instantiate Infrastructure classes in Application tests

## Application Test Rules

- Mock all interfaces from `Application/Common/Interfaces/`
- Test use cases in isolation and verify result shape and side effects
- Test validators using `TestValidate()` from `FluentValidation.TestHelper`
- Cover validation, failure, and cancellation-sensitive paths when behavior changes
- Add contract-focused tests when request or response mapping changes

## Integration Test Rules

- Use `WebApplicationFactory<T>` for full API tests
- Use a dedicated test database or in-memory equivalent
- Reset state between runs and avoid shared mutable state
- Cover the full slice from HTTP request through use-case flow to infrastructure
- Cover auth, serialization, configuration-driven behavior, and integration failure handling when those areas change

## General Rules

- Keep tests deterministic and avoid `DateTime.Now` without abstraction or random data without a stable seed
- Prefer `[Theory]` and `[InlineData]` for data-driven scenarios
- Keep setup minimal by using builders or factories for complex objects
- Changed behavior should have at least one happy-path test and one risk-relevant negative or edge-path test
