Под капотом в ASP NET Core представляет обычный лист

```csharp
public IServiceCollection Services => _serviceCollection;

public class ServiceCollection : IServiceCollection
{

}

public interface IServiceCollection : IList<ServiceDescriptor>  
{  
}

[DebuggerDisplay("{DebuggerToString(),nq}")]  
public class ServiceDescriptor  
{  
	public ServiceDescriptor(  
	Type serviceType [DynamicallyAccessedMembers(DynamicallyAccessedMemberTypes.PublicConstructors)] Type implementationType,  
	ServiceLifetime lifetime)  
	: this(serviceType, null, implementationType, lifetime)  
	{  
	}
}
```

^5011f3
