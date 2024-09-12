Dependency Injection - механизм, позволяющий в одном месте зарегистрировать любые классы в [[DI-контейнер]], а затем получать эти классы в любом месте приложения.

Более подробный код здесь: https://github.com/T0shik/raw-coding-101-tutorials/blob/main/Dependency%20Injection/resolver_container.linq
Видео: https://www.youtube.com/watch?v=NkTF_6IQPiY&t=5s

###  1. Регистрация сервисов в DI-контейнер

Cначала нужно положить сервисы в DI-контейнер:

```csharp
builder.Services.AddSingleton<DBStorage>();  
builder.Services.AddScoped<IProductService, ProductService>();  
builder.Services.AddScoped<ICartService, CartService>();
```

Внутри AddScoped сервис добавляется в лист DI-контейнера с указанием enum - Scoped (аналогично AddSingleton/AddTransient)
```csharp
public static IServiceCollection AddScoped(this IServiceCollection services, Type serviceType, Type implementationType)  
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
var parameters = ctor.GetParameters().ToArray();

// создаём нужные инстансы

if (parameters.Length > 0)
{
	var parametersImpl = new object[parameters.Length];

	for (int i = 0; i < parameters.Length; i++)
	{
		parametersImpl[i] =  GetService(parameters[i].ParameterType);
	}

	return Activator.CreateInstance(dependency, parametersImpl);
}

return Activator.CreateInstance(dependency);
```

После создания инстансы передаются в конструктор контроллера.

Слово Inject (инъекция, укол, вспрыск) - можно объяснить на примере

```csharp
public Person(Service service)

// в некоторых библиотеках можно встретить следующее
public Person([Inject]MyService service)
```
Пёрсону для существования жизненно необходим сервис. Поэтому мы берём из контейнера Service и втыкаем в пёрсона

### 3. Жизненный цикл зависимости

#### AddSingleton
Создаётся один раз при старте проекта и является общим (как будто статический класс)
#### AddScoped
В рамках одного запроса если мы много раз инжектим MyService в другие классы, то MyService будет всегда ссылаться на один и тот же объект в памяти (можно использовать как репозиторий для подключения к БД):
   
```csharp
builder.Services.AddScoped<MyService service>();

// везде будет ссылка на один и тот же объект в памяти
public Person(MyService service)
public Dog(MyService service)
public Cat(MyService service)
```

#### AddTransient
```csharp
builder.Services.AddTransient<MyService service>();

// у Person Cat Dog будут ссылки на разные объекты MyService
public Person(MyService service)
public Dog(MyService service)
public Cat(MyService service)
```
При каждой инъекции будет создаваться новый инстанс MyService. Таким образом каждый раз будет выделяться место в памяти под новый объект MyService


### Что происходит в конструкторе?

Если у нас есть конструктор:
```csharp
public FirstService(SecondService 2ndService){}
```

При этом `FirstService` нигде передаётся в конструктор, то как мы можем создать `FirstService` с использованием DI?

Для этого `FirstService` нужно обязательно поместить в DI контейнер и вместо `new FirstService()` вызывать `resolver.GetService<FirstService>`. Таким образом DI пройдётся по конструктору `FirstService` и создаст нужные зависимости. В случае  ASP NET Core, когда приходит запрос на контроллер, то фреймворк сам создаёт инстанс контроллера и с помощью DI смотрит зависимости в конструкторе и создаёт их.


