# Settings Patterns

## appsettings.json Structure

All custom keys use **camelCase**.

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*",
  "connection": {
    "database": "Host=...;Database=...;Username=...;Password=...",
    "hangfireDatabase": "Host=...;Database=...;Username=...;Password=...",
    "blobStorage": "DefaultEndpointsProtocol=https;AccountName=...;..."
  },
  "application": {
    "cacheDurationInHours": 12,
    "maxPageSize": 100,
    "defaultPageSize": 20
  }
}
```

---

## Strongly-Typed Options Classes

Location: `Application/Common/Options/`

### ConnectionOptions

```csharp
public class ConnectionOptions
{
    public const string SectionName = "connection";

    public string Database { get; set; } = string.Empty;
    public string HangfireDatabase { get; set; } = string.Empty;
    public string BlobStorage { get; set; } = string.Empty;
}
```

### ApplicationOptions

```csharp
public class ApplicationOptions
{
    public const string SectionName = "application";

    public int CacheDurationInHours { get; set; } = 12;
    public int MaxPageSize { get; set; } = 100;
    public int DefaultPageSize { get; set; } = 20;
}
```

---

## Registration Pattern

Bind options inside the relevant Infrastructure `DependencyInjection.cs` sub-method that owns that concern.
Do not bind options in a WebApi extensions file.

```csharp
// Inside the relevant private sub-method in Infrastructure/DependencyInjection.cs
services.Configure<ConnectionOptions>(
    configuration.GetSection(ConnectionOptions.SectionName));

services.Configure<ApplicationOptions>(
    configuration.GetSection(ApplicationOptions.SectionName));
```

---

## Usage in Infrastructure

```csharp
public class SomeService
{
    private readonly ConnectionOptions _connection;

    public SomeService(IOptions<ConnectionOptions> options)
        => _connection = options.Value;
}
```
