# Configure Application Settings Skill

## When to use

Adding or updating `appsettings` structure, options classes, or configuration binding.

## Load this additional guidance

Assume `@Backend-Engineer` has already loaded the core backend instructions.

- `instructions/cross-cutting/20-configuration.instructions.md`
- `instructions/cross-cutting/21-testing.instructions.md` when config behavior is tested
- `instructions/project/team-standards.instructions.md` when local config or secret-handling rules exist

## Patterns

- `patterns/configuration.pattern.md`

## Inputs

- setting name and purpose
- target section
- options class owner
- where the setting is consumed

## Steps

1. Decide whether the setting belongs under `connection` or `application`.
2. Update `appsettings` with camelCase keys.
3. Add or update strongly-typed options classes.
4. Bind configuration through `IOptions<T>` or the local standard.
5. Keep secrets out of committed files.
6. Note where the setting is consumed and how it affects behavior.
7. Suggest verification steps or tests when config changes behavior.

## Output

- setting summary
- section and options class used
- secret-handling notes
- verification or test notes

## Checklist

- [ ] Root section is correct
- [ ] Key casing is camelCase
- [ ] Strongly-typed options are used
- [ ] Secrets are handled safely
