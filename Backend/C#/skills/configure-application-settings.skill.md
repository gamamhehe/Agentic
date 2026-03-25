# Configure Application Settings Skill

## When to use

Adding or updating `appsettings` structure, options classes, or configuration binding.

## Instructions to load

- `instructions/core/01-architecture.instructions.md`
- `instructions/core/02-naming.instructions.md`
- `instructions/cross-cutting/20-configuration.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md` — when config tests in scope

## Patterns

- `patterns/configuration.pattern.md`

## Inputs

- Setting name and purpose
- Target root section (`connection` or `application`)
- Options class owner
- How the setting is consumed

## Steps

1. Decide `connection` or `application` section
2. Update `appsettings` with camelCase keys
3. Add or update strongly-typed options class
4. Bind via `IOptions<T>` registration
5. Ensure secrets not committed
6. Note where setting is consumed
7. Suggest verification or tests

## Checklist

- [ ] Root section correct
- [ ] Key casing camelCase
- [ ] Strongly-typed options used
- [ ] Secrets handled safely
