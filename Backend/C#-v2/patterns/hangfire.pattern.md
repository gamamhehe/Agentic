# Hangfire Patterns

## Job Class – Simple (no scoped dependencies)

Use when the job only needs singleton or transient dependencies.
Hangfire resolves job classes from DI automatically — no manual registration needed.
Place `[AutomaticRetry]` on the class; decorate the method when different retry policies per method are needed.
Accept `IJobCancellationToken` for graceful shutdown. Call `ThrowIfCancellationRequested()` at the start.

For fire-and-forget jobs that accept an entity id, use the same structure but replace `IJobCancellationToken` with `(Guid entityId, IJobCancellationToken cancellationToken)` — see **Enqueuing Jobs** below.

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

---

## Job Class – Scoped (EF Core repositories or scoped dependencies)

Use `IServiceScopeFactory` when the job needs EF Core repositories or any scoped dependency.
Create an async scope inside `ExecuteAsync` — never inject scoped services directly into the constructor.

Location: `Infrastructure/Services/HangfireJobService/`

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

---

## Enqueuing Jobs (Fire-and-Forget)

Use `IBackgroundJobClient` to enqueue a one-off job from application code.
Inject `IBackgroundJobClient` into the service or use-case that triggers the job.

```csharp
// Enqueue from a use-case or service
public class {UseCase}Handler
{
    private readonly IBackgroundJobClient _jobs;

    public {UseCase}Handler(IBackgroundJobClient jobs) => _jobs = jobs;

    public async Task Handle(...)
    {
        // ... business logic ...
        _jobs.Enqueue<{JobName}Job>(job => job.ExecuteAsync(entityId, JobCancellationToken.Null));
    }
}
```

---

## UseHangfireJobs Host Extension

Registers all **recurring** jobs in a single idempotent call on `IHost`.
Place in `Infrastructure/DependencyInjection.cs` (or a dedicated `HangfireExtensions.cs` alongside it).

Fire-and-forget jobs are enqueued at runtime via `IBackgroundJobClient` — they do not appear here.

Call order in `Program.cs`:

1. `app.UseAuthentication()`
2. `app.UseAuthorization()`
3. `app.UseHangfireDashboard()` _(optional)_
4. `app.UseHangfireJobs()` ← always last

`AddOrUpdate` is idempotent: creates the job on first run, updates the schedule on restart.
Use `JobCancellationToken.Null` when forwarding to `ExecuteAsync` from a recurring registration.

Location: `Infrastructure/DependencyInjection.cs`

```csharp
/// <summary>
/// Registers all Hangfire recurring jobs. Call this after <c>UseAuthorization()</c>
/// and <c>UseHangfireDashboard()</c> so the server is fully initialised.
/// <c>AddOrUpdate</c> is idempotent: creates on first run, updates the schedule on restart.
/// </summary>
public static IHost UseHangfireJobs(this IHost host)
{
    var jobs = host.Services.GetRequiredService<IRecurringJobManager>();

    jobs.AddOrUpdate<{JobName}Job>(
        "{job-name}",
        job => job.ExecuteAsync(JobCancellationToken.Null),
        Cron.Daily);

    // Add further recurring jobs here - one AddOrUpdate call per job.

    return host;
}
```

---

## Dashboard Access Control (optional)

Restrict the Hangfire dashboard to authenticated admin users only.

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
