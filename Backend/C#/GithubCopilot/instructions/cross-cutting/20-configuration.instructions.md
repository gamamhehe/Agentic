---
name: Configuration-Instructions
description: Rules for appsettings structure, options classes, and secrets management.
applyTo: "**/appsettings*.json"
---

# Configuration Instructions

See `patterns/configuration.pattern.md` for code examples.

## Structure Rules

Two root sections in `appsettings.json`:

| Section         | Purpose                                                                                |
| --------------- | -------------------------------------------------------------------------------------- |
| `"connection"`  | All connection strings and endpoints (database, cache, blob, external APIs)            |
| `"application"` | All logic settings (feature flags, retry policies, cache durations, business defaults) |

`Logging` and `AllowedHosts` remain at root level per ASP.NET Core convention.

## JSON Key Casing

All custom keys: **camelCase** (e.g. `"cacheDurationInHours"`, `"maxPageSize"`)

## Rules

1. Never place connection strings outside `"connection"`
2. Never place logic settings inside `"connection"`
3. Use strongly-typed options via `IOptions<T>`
4. Read connection strings via `configuration.GetSection("connection")["database"]` or options class
5. Sensitive values: User Secrets in dev, environment variables or Key Vault in production — never commit real credentials
6. `appsettings.Development.json` follows the same section structure

## Options Classes

| Class                | Section         | Location                      |
| -------------------- | --------------- | ----------------------------- |
| `ConnectionOptions`  | `"connection"`  | `Application/Common/Options/` |
| `ApplicationOptions` | `"application"` | `Application/Common/Options/` |

## API Key

- Under `"application"` as `apiKey`
- Never commit real values
- `ApplicationOptions` exposes `ApiKey` property bound to `application:apiKey`
