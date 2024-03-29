Под капотом в ASP NET Core представляет обычный лист куда складываются все зарегистрированные сервисы.

```csharp
public IServiceCollection Services => _serviceCollection;

public class ServiceCollection : IServiceCollection
{
}

public interface IServiceCollection : IList<ServiceDescriptor>  
{  
}
```

^5011f3
ServiceDescriptor - это конкретно то, что лежит в DI-контейнере. Содержит:

serviceType - тип интерфейса
implementationType - тип реализации
lifetime - [[DI#3. Жизненный цикл зависимости]]

```csharp
public class ServiceDescriptor  
{  
	public ServiceDescriptor(Type serviceType,  Type implementationType,  erviceLifetime lifetime)  
	: this(serviceType, null, implementationType, lifetime)  
	{  
	}
}
```
Например:
```csharp
builder.Services.AddScoped<IProductService, ProductService>();

serviceType - IProductService
implementationType - ProductService
lifetime - Scoped
```