# Application Patterns

## UseCase Contract (SharedKernel)

Location: `src/{ProjectName}.SharedKernel/IUseCase.cs`

```csharp
namespace {ProjectName}.SharedKernel;

public interface IUseCase
{
}

public interface IUseCase<TRequest, TResponse> : IUseCase
{
    Task<TResponse> ExecuteAsync(TRequest request, CancellationToken ct = default);
}

public interface IUseCase<TRequest1, TRequest2, TResponse> : IUseCase
{
    Task<TResponse> ExecuteAsync(TRequest1 request1, TRequest2 request2, CancellationToken ct = default);
}
```

## Business Context UseCase

Location: `Application/Features/{BusinessContext}/UseCases/{UseCaseName}.cs`

```csharp
namespace {ProjectName}.Application.Features.Orders.UseCases;

public sealed class UpsertOrder(
    IOrderRepository repository,
    IUserContext userContext)
    : IUseCase<Guid, UpsertOrder.Request, Guid>
{
    public async Task<Guid> ExecuteAsync(Guid id, Request request, CancellationToken ct = default)
    {
        ArgumentNullException.ThrowIfNull(request);

        var currentUserId = userContext.UserId;
        var order = request.ToDomain(id, currentUserId);

        return await repository.UpsertAsync(order, ct);
    }

    public sealed record Request(string Number, DateTime OrderedAt)
    {
        public Order ToDomain(Guid id, Guid userId)
            => new(id, Number, OrderedAt, userId);
    }
}
```

## FluentValidation for UseCase Request

Location: `Application/Features/{BusinessContext}/Validator/{UseCaseName}Validator.cs`

```csharp
using FluentValidation;
using static {ProjectName}.Application.Features.Orders.UseCases.UpsertOrder;

namespace {ProjectName}.Application.Features.Orders.Validator;

public sealed class UpsertOrderValidator : AbstractValidator<Request>
{
    public UpsertOrderValidator()
    {
        RuleFor(x => x.Number)
            .NotEmpty()
            .MaximumLength(32);

        RuleFor(x => x.OrderedAt)
            .LessThanOrEqualTo(DateTime.UtcNow.AddMinutes(1));
    }
}
```

## Automatic UseCase Registration Extension

Location: `Application/Common/DependencyInjection/UseCaseRegistrationExtensions.cs`

```csharp
using System.Reflection;
using Microsoft.Extensions.DependencyInjection;

public static class UseCaseRegistrationExtensions
{
    public static IServiceCollection AddUseCasesFromAssembly(
        this IServiceCollection services,
        Assembly assembly)
    {
        var implementationTypes = assembly
            .DefinedTypes
            .Where(t => t is { IsClass: true, IsAbstract: false })
            .Where(t => typeof(IUseCase).IsAssignableFrom(t.AsType()))
            .ToList();

        foreach (var implementation in implementationTypes)
        {
            var implementationType = implementation.AsType();

            services.AddScoped(implementationType);

            var contracts = implementation
                .ImplementedInterfaces
                .Where(i => i != typeof(IUseCase) && typeof(IUseCase).IsAssignableFrom(i));

            foreach (var contract in contracts)
            {
                services.AddScoped(contract, sp => sp.GetRequiredService(implementationType));
            }
        }

        return services;
    }
}
```

## Automatic FluentValidation Integration in UseCase Flow

Location: `Application/Common/Execution/ValidatedUseCaseDecorator.cs`

```csharp
using FluentValidation;
using FluentValidation.Results;

public sealed class ValidatedUseCaseDecorator<TRequest, TResponse>(
    IUseCase<TRequest, TResponse> inner,
    IEnumerable<IValidator<TRequest>> validators)
    : IUseCase<TRequest, TResponse>
{
    public async Task<TResponse> ExecuteAsync(TRequest request, CancellationToken ct = default)
    {
        if (validators.Any())
        {
            var context = new ValidationContext<TRequest>(request);
            var validationResults = await Task.WhenAll(validators.Select(v => v.ValidateAsync(context, ct)));

            var failures = validationResults
                .SelectMany(static x => x.Errors)
                .Where(static x => x is not null)
                .ToList();

            if (failures.Count > 0)
            {
                throw new ValidationException(failures);
            }
        }

        return await inner.ExecuteAsync(request, ct);
    }
}
```

Location: `Application/DependencyInjection.cs`

```csharp
using FluentValidation;
using Microsoft.Extensions.DependencyInjection;
using Scrutor;

public static class DependencyInjection
{
    public static IServiceCollection AddApplication(this IServiceCollection services)
    {
        var assembly = typeof(DependencyInjection).Assembly;

        services.AddUseCasesFromAssembly(assembly);
        services.AddValidatorsFromAssembly(assembly);

        services.TryDecorate(typeof(IUseCase<,>), typeof(ValidatedUseCaseDecorator<,>));

        return services;
    }
}
```

## Interactor/Executor Pattern (Optional)

Location: `src/{ProjectName}.SharedKernel/IInteractor.cs` (contract)

Location: `src/{ProjectName}.Infrastructure/Execution/Interactor.cs` (implementation)

```csharp
public interface IInteractor
{
    TUseCase Create<TUseCase>() where TUseCase : IUseCase;
}

```

```csharp
public sealed class Interactor(IServiceProvider serviceProvider) : IInteractor
{
    public TUseCase Create<TUseCase>() where TUseCase : IUseCase
        => serviceProvider.GetRequiredService<TUseCase>();
}
```

Use this when you want controllers/endpoints to resolve concrete UseCase types by class name, similar to the Rotte style.
