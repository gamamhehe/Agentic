# Configuration Patterns

## appsettings.json Structure

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

## Strongly-Typed Options

Location: `Application/Common/Options/`

```csharp
public class ConnectionOptions
{
    public const string SectionName = "connection";

    public string Database { get; set; } = string.Empty;
    public string HangfireDatabase { get; set; } = string.Empty;
    public string BlobStorage { get; set; } = string.Empty;
}
```

```csharp
public class ApplicationOptions
{
    public const string SectionName = "application";

    public int CacheDurationInHours { get; set; } = 12;
    public int MaxPageSize { get; set; } = 100;
    public int DefaultPageSize { get; set; } = 20;
}
```

## Registration

Bind in the relevant Infrastructure DI sub-method.

```csharp
services.Configure<ConnectionOptions>(
    configuration.GetSection(ConnectionOptions.SectionName));

services.Configure<ApplicationOptions>(
    configuration.GetSection(ApplicationOptions.SectionName));
```

## Usage

```csharp
public class SomeService
{
    private readonly ConnectionOptions _connection;

    public SomeService(IOptions<ConnectionOptions> options)
        => _connection = options.Value;
}
```
