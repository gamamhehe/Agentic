# Testing Patterns

## Unit Test — UseCase

```csharp
using FluentAssertions;
using NSubstitute;

public class Get{Entity}ByIdTests
{
    private readonly I{Entity}Repository _repository = Substitute.For<I{Entity}Repository>();
    private readonly Get{Entity}ById _useCase;

    public Get{Entity}ByIdTests() => _useCase = new(_repository);

    [Fact]
    public async Task ExecuteAsync_WhenEntityExists_ShouldReturnDto()
    {
        var id = Guid.NewGuid();
        _repository.GetByIdAsync(id, Arg.Any<CancellationToken>())
            .Returns(new {Entity} { Id = id });

        var result = await _useCase.ExecuteAsync(new Get{Entity}ById.Request(id), CancellationToken.None);

        result.Should().NotBeNull();
        result!.Id.Should().Be(id);
    }

    [Fact]
    public async Task ExecuteAsync_WhenEntityNotFound_ShouldReturnNull()
    {
        _repository.GetByIdAsync(Arg.Any<Guid>(), Arg.Any<CancellationToken>())
            .Returns(({Entity}?)null);

        var result = await _useCase.ExecuteAsync(new Get{Entity}ById.Request(Guid.NewGuid()), CancellationToken.None);

        result.Should().BeNull();
    }
}
```

## Unit Test — FluentValidation Validator

```csharp
using FluentValidation.TestHelper;

public class {UseCaseName}ValidatorTests
{
    private readonly {UseCaseName}Validator _validator = new();

    [Fact]
    public void Validate_WhenAllFieldsValid_ShouldPass()
    {
        var result = _validator.TestValidate(new {UseCaseName}.Request(/* valid props */));
        result.ShouldNotHaveAnyValidationErrors();
    }

    [Fact]
    public void Validate_WhenIdIsEmpty_ShouldFailOnId()
    {
        var result = _validator.TestValidate(new {UseCaseName}.Request(Guid.Empty, ""));
        result.ShouldHaveValidationErrorFor(x => x.Id);
    }
}
```

## Integration Test — API Endpoint

```csharp
public class {DomainModel}EndpointsTests : IClassFixture<WebApplicationFactory<Program>>
{
    private readonly HttpClient _client;

    public {DomainModel}EndpointsTests(WebApplicationFactory<Program> factory)
        => _client = factory.CreateClient();

    [Fact]
    public async Task Get_WhenEntityExists_ShouldReturn200()
    {
        var id = Guid.NewGuid(); // pre-seeded in test DB

        var response = await _client.GetAsync($"/api/v1/{domainmodel}/{id}");

        response.StatusCode.Should().Be(HttpStatusCode.OK);
    }
}
```
