# API Patterns

## Minimal API Endpoint with UseCase Interface

```csharp
using Microsoft.AspNetCore.Http.HttpResults;

public static class OrdersEndpoints
{
    public static void MapOrdersEndpoints(this IEndpointRouteBuilder app)
    {
        var group = app.MapGroup("/api/v1/orders").WithTags("Orders");

        group.MapGet("/{id:guid}", async (
            Guid id,
            IUseCase<GetOrderById.Request, GetOrderById.Response?> useCase,
            CancellationToken ct) =>
        {
            var result = await useCase.ExecuteAsync(new GetOrderById.Request(id), ct);
            return result is not null ? TypedResults.Ok(result) : TypedResults.NotFound();
        })
        .WithName("GetOrderById")
        .Produces<GetOrderById.Response>(StatusCodes.Status200OK)
        .ProducesProblem(StatusCodes.Status404NotFound);
    }
}
```

## MVC Controller with Interactor (Rotte-style)

```csharp
[ApiController]
[Route("[controller]")]
public class OrdersController(IInteractor interactor) : ControllerBase
{
    [HttpPost]
    public async Task<IActionResult> UpsertAsync([FromBody] UpsertOrder.Request request, CancellationToken ct)
    {
        var id = await interactor
            .Create<UpsertOrder>()
            .ExecuteAsync(Guid.Empty, request, ct);

        return Ok(id);
    }
}
```

## OpenAPI / Scalar Setup

File: `{ProjectName}.WebApi/Extensions/OpenApiExtensions.cs`

```csharp
// Program.cs
builder.Services.AddOpenApiServices();

app.UseAuthentication();
app.UseAuthorization();
app.UseOpenApiPipeline();
```

```csharp
public static class OpenApiExtensions
{
    public static IServiceCollection AddOpenApiServices(this IServiceCollection services)
    {
        services.AddOpenApi(options =>
        {
            options.AddOperationTransformer<AddApiHeaderParameter>();

            options.AddDocumentTransformer((document, context, cancellationToken) =>
            {
                document.Servers =
                [
                    new() { Url = "{ProjectRouteInCustomDNS}", Description = "Production" },
                    new() { Url = "/", Description = "Root" }
                ];
                document.Info = new()
                {
                    Title = "",
                    Version = "v1",
                    Description = "API for "
                };
                return Task.CompletedTask;
            });
        });
        return services;
    }

    public static WebApplication UseOpenApiPipeline(this WebApplication app)
    {
        app.MapOpenApi();
        app.MapScalarApiReference();
        return app;
    }
}
```
