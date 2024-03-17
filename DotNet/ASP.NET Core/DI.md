Dependency Injection - механизм, позволяющий зарегистрировать любой класс в DI-контейнере, а затем получить любой сервис из [[DI-контейнер]].


1) Cначала нужно положить сервисы в [[DI-контейнер]] ()
1) Этап регистрации сервисов:

```csharp
builder.Services.AddSingleton<DBStorage>();  
builder.Services.AddScoped<IProductService, ProductService>();  
builder.Services.AddScoped<ICartService, CartService>();
```