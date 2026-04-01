# Structure Pattern

```plaintext
repository-name/
├── src/
│   ├── {ProjectName}.Domain/
│   │   ├── Common/
│   │   ├── Exceptions/
│   │   ├── Models/
│   │   └── Utils/
│   │
│   ├── {ProjectName}.SharedKernel/
│   │   ├── IUseCase.cs
│   │   ├── IInteractor.cs
│   │   └── Common/
│   │
│   ├── {ProjectName}.Application/
│   │   ├── Common/
│   │   │   ├── Execution/
│   │   │   ├── Interfaces/
│   │   │   └── Options/
│   │   ├── Features/
│   │   │   ├── {BusinessContextA}/
│   │   │   │   ├── UseCases/
│   │   │   │   │   ├── {UseCaseName}.cs
│   │   │   │   │   └── {AnotherUseCaseName}.cs
│   │   │   │   ├── Validator/
│   │   │   │   │   └── {UseCaseName}Validator.cs
│   │   │   │   └── Dtos/
│   │   │   └── {BusinessContextB}/
│   │   └── Utils/
│   │
│   ├── {ProjectName}.Infrastructure/
│   │   ├── ApplicationInsights/
│   │   ├── Caches/
│   │   ├── Files/
│   │   ├── Services/
│   │   │   └── HangfireJobService/
│   │   ├── Persistence/
│   │   │   ├── Configurations/
│   │   │   └── Repositories/
│   │   ├── Migrations/
│   │   │   └── DBScripts/
│   │   └── DependencyInjection.cs
│   │
│   └── {ProjectName}.WebApi/
│       ├── Endpoints/
│       ├── Extensions/
│       └── Middleware/
│
├── tests/
│   ├── {ProjectName}.Domain.Tests/
│   ├── {ProjectName}.Application.Tests/
│   └── {ProjectName}.IntegrationTests/
│
├── .gitignore
├── docker-compose.yml
├── {ProjectName}.slnx
└── README.md
```
