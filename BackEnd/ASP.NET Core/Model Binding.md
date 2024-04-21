### By Default
Если параметр примитивного типа, то пытаемся получить значение из [[URI]]

Пример:
```csharp
HttpResponseMessage Put(int id, Product item) { ... }
```

`id` - примитивный тип, поэтому Web API пытается получить значение из [[URI]]
`item` - сложный тип, поэтому Web API использует [[Media-type formatter]] чтобы прочитать значение из [[Request body]]

Чтобы извлечь значение из [[URI]], Web API смотрит в [[Route data]] и в [[Query string]]. 