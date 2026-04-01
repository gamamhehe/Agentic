# Hangfire Patterns

## Simple Job (no scoped dependencies)

Location: `Infrastructure/Services/HangfireJobService/`

```csharp
using Hangfire;

[AutomaticRetry(Attempts = 3)]
public class {JobName}Job
{
    private readonly ILogger<{JobName}Job> _logger;

    public {JobName}Job(ILogger<{JobName}Job> logger) => _logger = logger;

    public async Task ExecuteAsync(IJobCancellationToken cancellationToken)
    {
        cancellationToken.ThrowIfCancellationRequested();
        _logger.LogInformation("Starting {JobName} job.");

        // job logic here

        _logger.LogInformation("{JobName} job completed.");
    }
}
```

## Scoped Job (EF Core or scoped dependencies)

Use `IServiceScopeFactory` — never inject scoped services directly.

```csharp
using Hangfire;
using Microsoft.Extensions.DependencyInjection;

[AutomaticRetry(Attempts = 3)]
public class {JobName}Job
{
    private readonly IServiceScopeFactory _scopeFactory;
    private readonly ILogger<{JobName}Job> _logger;

    public {JobName}Job(IServiceScopeFactory scopeFactory, ILogger<{JobName}Job> logger)
    {
        _scopeFactory = scopeFactory;
        _logger = logger;
    }

    public async Task ExecuteAsync(IJobCancellationToken cancellationToken)
    {
        cancellationToken.ThrowIfCancellationRequested();

        await using var scope = _scopeFactory.CreateAsyncScope();
        var repository = scope.ServiceProvider.GetRequiredService<I{Entity}Repository>();

        // implementation logic using repository
        _logger.LogInformation("{JobName}Job completed.");
    }
}
```

## Enqueuing Fire-and-Forget Jobs

```csharp
public class {UseCase}
{
    private readonly IBackgroundJobClient _jobs;

    public {UseCase}(IBackgroundJobClient jobs) => _jobs = jobs;

    public async Task ExecuteAsync(...)
    {
        // ... business logic ...
        _jobs.Enqueue<{JobName}Job>(job => job.ExecuteAsync(entityId, JobCancellationToken.Null));
    }
}
```

## Recurring Jobs Registration

Location: `Infrastructure/DependencyInjection.cs`

Call order in `Program.cs`: `UseAuthentication()` → `UseAuthorization()` → `UseHangfireDashboard()` → `UseHangfireJobs()`

```csharp
public static IHost UseHangfireJobs(this IHost host)
{
    var jobs = host.Services.GetRequiredService<IRecurringJobManager>();

    jobs.AddOrUpdate<{JobName}Job>(
        "{job-name}",
        job => job.ExecuteAsync(JobCancellationToken.Null),
        Cron.Daily);

    // one AddOrUpdate call per recurring job

    return host;
}
```

## Dashboard Access Control (optional)

```csharp
app.UseHangfireDashboard("/hangfire", new DashboardOptions
{
    Authorization = [new HangfireAuthorizationFilter()]
});
```

```csharp
public class HangfireAuthorizationFilter : IDashboardAuthorizationFilter
{
    public bool Authorize(DashboardContext context)
    {
        var httpContext = context.GetHttpContext();
        return httpContext.User.Identity?.IsAuthenticated == true
            && httpContext.User.IsInRole("Admin");
    }
}
```
