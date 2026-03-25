# Entity Framework Core Patterns

## Audit Fields in SaveChangesAsync

```csharp
public override async Task<int> SaveChangesAsync(CancellationToken cancellationToken = default)
{
    var now = dateTimeProvider.UtcNow;
    var userId = userContext.UserId;

    foreach (var entry in ChangeTracker.Entries<BaseEntity>())
    {
        switch (entry.State)
        {
            case EntityState.Added:
                entry.Entity.CreatedBy = userId;
                entry.Entity.CreatedAt = now;
                entry.Entity.UpdatedBy = userId;
                entry.Entity.UpdatedAt = now;
                break;

            case EntityState.Modified:
                entry.Property(x => x.CreatedBy).IsModified = false;
                entry.Property(x => x.CreatedAt).IsModified = false;
                entry.Entity.UpdatedBy = userId;
                entry.Entity.UpdatedAt = now;
                break;
        }
    }

    var result = await base.SaveChangesAsync(cancellationToken);
    await DispatchDomainEvents();
    return result;
}
```

## Entity Configuration

Location: `Infrastructure/Persistence/Configurations/`

```csharp
using Microsoft.EntityFrameworkCore;
using Microsoft.EntityFrameworkCore.Metadata.Builders;

public class {Entity}Configuration : IEntityTypeConfiguration<{Entity}>
{
    public void Configure(EntityTypeBuilder<{Entity}> builder)
    {
        builder.ToTable("{Entity}s");
        builder.HasKey(e => e.Id);
        builder.Property(e => e.Name).IsRequired().HasMaxLength(200);
        builder.Property(e => e.CreatedBy).IsRequired().HasMaxLength(200);
        builder.Property(e => e.UpdatedBy).IsRequired().HasMaxLength(200);
    }
}
```
