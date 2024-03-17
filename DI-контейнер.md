Под капотом в ASP NET Core представляет обычный лист

```csharp
public IServiceCollection Services => _serviceCollection;

public class ServiceCollection : IServiceCollection
{

}

public interface IServiceCollection : IList<ServiceDescriptor>  
{  
}

```