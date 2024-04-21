### By Default
Если параметр примитивного типа, то пытаемся получить значение из [[URI]]

Пример:
```csharp
HttpResponseMessage Put(int id, Product item) { ... }
```

`id` - примитивный тип, поэтому WebApi пыат