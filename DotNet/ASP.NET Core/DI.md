Dependency Injection - механизм, позволяющий зарегистрировать любой класс в DI-контейнере, а затем получить любой сервис из [[DI-контейнер]].

Более подробный код здесь: https://github.com/T0shik/raw-coding-101-tutorials/blob/main/Dependency%20Injection/resolver_container.linq
Видео: https://www.youtube.com/watch?v=NkTF_6IQPiY&t=5s

###  1. Регистрация сервисов в DI-контейнер

Cначала нужно положить сервисы в [[DI-контейнер]] ()

```csharp
builder.Services.AddSingleton<DBStorage>();  
builder.Services.AddScoped<IProductService, ProductService>();  
builder.Services.AddScoped<ICartService, CartService>();
```

Внутри AddScoped сервис добавляется в лист [[DI-контейнер#^5011f3]] с указанием enum - Scoped
```csharp
public static IServiceCollection AddScoped(  
this IServiceCollection services,  
Type serviceType,  
[DynamicallyAccessedMembers(DynamicallyAccessedMemberTypes.PublicConstructors)] Type implementationType)  
{  
	ThrowHelper.ThrowIfNull(services);  
	ThrowHelper.ThrowIfNull(serviceType);  
	ThrowHelper.ThrowIfNull(implementationType);  
	  
	return Add(services, serviceType, implementationType, ServiceLifetime.Scoped);  
}
```

### 2. Инъекция в конструкторе

После регистрации сервисов можно получить любой зарегистрированный сервис в конструкторе класса

```csharp
public HomeController(IProductService productService)  
{  
	_productService = productService;  
}
```

Под капотом фреймворк ASP NET Core происходит следующее:
1. Приходит запрос на контроллер Home
2. Фреймворк создаёт новый инстанс контроллера (тут DI ещё не используется)
3. Начинает работать рефлексия:



```csharp
// получаем конструктор контроллера
var dependency = GetDependency(type)
var ctor = dependency.GetConstructors().Single();

// получаем параметры конструктора
constructor.GetParameters().ToArray();
```

