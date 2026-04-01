# Infrastructure Patterns

## Memory Cache Service

Location: `Infrastructure/Caches/`

```csharp
using Microsoft.Extensions.Caching.Memory;

public class {Entity}CacheService
{
    private readonly IMemoryCache _cache;
    private readonly I{Entity}Repository _repository;
    private const string CacheKey = "{Entity}_List";

    public {Entity}CacheService(IMemoryCache cache, I{Entity}Repository repository)
    {
        _cache = cache;
        _repository = repository;
    }

    public async Task<IReadOnlyList<{Entity}Dto>> GetAllAsync(CancellationToken ct)
        => await _cache.GetOrCreateAsync(CacheKey, async entry =>
        {
            entry.AbsoluteExpirationRelativeToNow = TimeSpan.FromHours(12);
            return await _repository.GetAllActiveAsync(ct);
        }) ?? [];
}
```

## Refit HTTP Client with Auth Interceptor

Location: `Infrastructure/Services/`

```csharp
using System.Net.Http.Headers;

public class AuthHeaderHandler : DelegatingHandler
{
    private readonly ITokenService _tokenService;

    public AuthHeaderHandler(ITokenService tokenService)
        => _tokenService = tokenService;

    protected override async Task<HttpResponseMessage> SendAsync(
        HttpRequestMessage request, CancellationToken cancellationToken)
    {
        var token = await _tokenService.GetAccessTokenAsync(cancellationToken);
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", token);
        return await base.SendAsync(request, cancellationToken);
    }
}
```

## Repository Implementation

Location: `Infrastructure/Persistence/Repositories/`

```csharp
using Microsoft.EntityFrameworkCore;

public class {Entity}Repository : I{Entity}Repository
{
    private readonly ApplicationDbContext _context;

    public {Entity}Repository(ApplicationDbContext context)
        => _context = context;

    public async Task<{Entity}?> GetByIdAsync(Guid id, CancellationToken ct)
        => await _context.{Entity}s
            .AsNoTracking()
            .FirstOrDefaultAsync(e => e.Id == id, ct);

    public async Task<List<{Entity}>> GetAllAsync(CancellationToken ct)
        => await _context.{Entity}s
            .AsNoTracking()
            .ToListAsync(ct);

    public async Task AddAsync({Entity} entity, CancellationToken ct)
    {
        await _context.{Entity}s.AddAsync(entity, ct);
        await _context.SaveChangesAsync(ct);
    }

    public async Task UpdateAsync({Entity} entity, CancellationToken ct)
    {
        _context.{Entity}s.Update(entity);
        await _context.SaveChangesAsync(ct);
    }

    public async Task DeleteAsync({Entity} entity, CancellationToken ct)
    {
        _context.{Entity}s.Remove(entity);
        await _context.SaveChangesAsync(ct);
    }
}
```

## Dependency Injection — Entry Orchestrator

Location: `Infrastructure/DependencyInjection.cs`

```csharp
public static IServiceCollection AddInfrastructureServices(
    this IServiceCollection services,
    IConfiguration configuration)
{
    AddDatabase(services, configuration);
    AddRepositories(services);
    AddCoreServices(services);
    AddHttpClients(services);
    AddCaching(services);
    AddAuthentication(services, configuration);
    AddBlobStorage(services, configuration);
    AddObservability(services, configuration);
    AddHangfire(services, configuration);

    return services;
}
```

### AddDatabase

```csharp
private static void AddDatabase(IServiceCollection services, IConfiguration configuration)
{
    var connectionString = configuration.GetSection("connection")["database"];
    services.AddDbContext<ApplicationDbContext>(options =>
        options.UseNpgsql(connectionString));
    services.AddScoped<IApplicationDbContext>(sp =>
        sp.GetRequiredService<ApplicationDbContext>());
}
```

### AddRepositories

```csharp
private static void AddRepositories(IServiceCollection services)
{
    services.AddScoped<IDocumentRepository, DocumentRepository>();
    // one line per repository
}
```

### AddCoreServices

```csharp
private static void AddCoreServices(IServiceCollection services)
{
    services.AddHttpContextAccessor();
    services.AddScoped<IUserContext, UserContext>();
    services.AddScoped<IDocumentExpiryNotificationService, DocumentExpiryNotificationService>();
}
```

### AddHttpClients

```csharp
private static void AddHttpClients(IServiceCollection services)
{
    services.AddHttpClient<ILinkCheckService, LinkCheckService>(client =>
    {
        client.Timeout = TimeSpan.FromSeconds(10);
    });

    services.AddHttpClient<IExternalApiClient, ExternalApiClient>(client =>
    {
        client.BaseAddress = new Uri("https://api.example.com");
        client.Timeout = TimeSpan.FromSeconds(30);
    })
    .AddHttpMessageHandler<AuthHeaderHandler>();
}
```

### AddCaching

```csharp
private static void AddCaching(IServiceCollection services)
{
    services.AddMemoryCache(options =>
    {
        options.SizeLimit = 1000;
        options.CompactionPercentage = 0.25;
        options.ExpirationScanFrequency = TimeSpan.FromMinutes(5);
    });
    services.AddSingleton<ICacheService, MemoryCacheService>();
}
```

### AddAuthentication

```csharp
private static void AddAuthentication(
    IServiceCollection services,
    IConfiguration configuration)
{
    services.Configure<IdentityOptions>(
       configuration.GetSection(IdentityOptions.SectionName));
    var identityConfig = configuration.GetSection(IdentityOptions.SectionName)
        .Get<IdentityOptions>()
        ?? throw new InvalidOperationException("IdentityOptions configuration is missing.");

    if (string.IsNullOrWhiteSpace(identityConfig.Authority)
        || string.IsNullOrWhiteSpace(identityConfig.Audience))
    {
        services.AddAuthorization();
        return;
    }

    services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
        .AddJwtBearer(options =>
        {
            options.Authority = identityConfig.Authority;
            options.Audience = identityConfig.Audience;
            options.IncludeErrorDetails = true;
            options.RequireHttpsMetadata = true;

            options.TokenValidationParameters = new TokenValidationParameters
            {
                ValidIssuer = identityConfig.Authority,
                ValidAudience = identityConfig.Audience,
                ValidateIssuer = true,
                ValidateAudience = true,
                ValidateLifetime = true,
                ValidateIssuerSigningKey = true
            };

            options.Events = new JwtBearerEvents
            {
                OnAuthenticationFailed = context =>
                {
                    context.Response.StatusCode = StatusCodes.Status401Unauthorized;
                    context.Response.ContentType = "application/json";
                    return context.Response.WriteAsync(
                        JsonSerializer.Serialize(new { error = "Authentication failed." }));
                }
            };
        });

    services.AddAuthorization();
}
```

### AddBlobStorage

```csharp
private static void AddBlobStorage(
    IServiceCollection services,
    IConfiguration configuration)
{
    var connectionString = configuration.GetConnectionString("AzureStorage");
    if (string.IsNullOrWhiteSpace(connectionString)) return;

    services.Configure<AzureStorageOptions>(
        configuration.GetSection(AzureStorageOptions.SectionName));
    services.AddSingleton(_ => new BlobServiceClient(connectionString));
    services.AddScoped<IBlobStorageService, AzureBlobStorageService>();
}
```

### AddObservability

```csharp
private static void AddObservability(
    IServiceCollection services,
    IConfiguration configuration)
{
    services.AddApplicationInsightsTelemetry(configuration);
    services.AddTransient<RequestBodyLoggingMiddleware>();
    services.AddTransient<ApiTrackingEndpointFilter>();
}
```

### AddHangfire

```csharp
private static void AddHangfire(
    IServiceCollection services,
    IConfiguration configuration)
{
    var connectionString = configuration.GetConnectionString("HangfireDb");
    if (string.IsNullOrWhiteSpace(connectionString)) return;

    services.AddHangfire(config => config
        .SetDataCompatibilityLevel(CompatibilityLevel.Version_180)
        .UseSimpleAssemblyNameTypeSerializer()
        .UseRecommendedSerializerSettings()
        .UseSqlServerStorage(connectionString));
    services.AddHangfireServer();
}
```
