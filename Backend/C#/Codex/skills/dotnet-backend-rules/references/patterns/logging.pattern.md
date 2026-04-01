# Logging Patterns

## Layer Placement

- **Infrastructure** — telemetry implementation under `Infrastructure/ApplicationInsights/`
- **WebApi** — only wires middleware into pipeline

## DI Registration

```csharp
private static void AddObservability(IServiceCollection services, IConfiguration configuration)
{
    services.AddApplicationInsightsTelemetry(configuration);
    services.AddTransient<RequestBodyLoggingMiddleware>();
    services.AddTransient<ApiTrackingEndpointFilter>();
}
```

## WebApi Pipeline Order

```csharp
app.UseRouting();
app.UseMiddleware<RequestBodyLoggingMiddleware>();
app.UseAuthentication();
app.UseAuthorization();
```

## Endpoint Tracking

```csharp
group.MapPost("/", handler)
    .WithName("CreateOrder")
    .WithApiTracking("CreateOrder", "MyEpic", "Create")
    .Produces<Guid>(201);
```

## ApiTrackingActionFilter — Endpoint Metadata Marker

```csharp
namespace {ProjectName}.Infrastructure.ApplicationInsights;

[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, AllowMultiple = true)]
public sealed class ApiTrackingActionFilter : Attribute
{
    public ApiTrackingActionFilter(string funcName, string epicName, string feature) { ... }
    public string FuncName { get; }
    public string EpicName { get; }
    public string Feature { get; }
}
```

## ApiTrackingEndpointFilter — Telemetry Enrichment

`IEndpointFilter` that measures duration, writes properties to `RequestTelemetry`, fires `TelemetryClient.TrackEvent`.

## RequestBodyLoggingMiddleware — Request Body Capture

Reads POST/PUT bodies into `RequestTelemetry.Properties["RequestBody"]` only when endpoint has `ApiTrackingActionFilter` metadata.

```csharp
if (context.GetEndpoint()?.Metadata.GetMetadata<ApiTrackingActionFilter>() is not null)
{
    requestTelemetry?.Properties.TryAdd("RequestBody", requestBody);
}
```

## ApiTrackingExtensions — Fluent Wiring

```csharp
public static RouteHandlerBuilder WithApiTracking(
    this RouteHandlerBuilder builder,
    string funcName, string epicName, string feature)
{
    return builder
        .WithMetadata(new ApiTrackingActionFilter(funcName, epicName, feature))
        .AddEndpointFilter<ApiTrackingEndpointFilter>();
}
```

## Telemetry Properties

| Property        | Source            | Description             |
| --------------- | ----------------- | ----------------------- |
| `Function`      | `funcName`        | Endpoint/operation name |
| `Epic`          | `epicName`        | Business epic grouping  |
| `Feature`       | `feature`         | Feature category        |
| `IsSuccess`     | Try/catch         | True or False           |
| `Duration`      | Stopwatch         | Execution time ms       |
| `Date`          | `DateTime.UtcNow` | UTC ISO 8601            |
| `RequestBody`   | Middleware        | POST/PUT body           |
| `ResponseBody`  | Filter            | Response object         |
| `UserIpAddress` | `RemoteIpAddress` | Client IP               |
| `TenantId`      | Claim/header      | Tenant identifier       |

## appsettings.json

```json
{
  "ApplicationInsights": {
    "ConnectionString": "InstrumentationKey=...;IngestionEndpoint=https://..."
  }
}
```
