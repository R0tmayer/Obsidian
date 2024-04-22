### By Default
Если параметр примитивного типа, то пытаемся получить значение из [[URI]]

Пример:
```csharp
HttpResponseMessage Put(int id, Product item) { ... }
```

`id` - примитивный тип, поэтому Web API пытается получить значение из [[URI]]
`item` - сложный тип, поэтому Web API использует [[Media-type formatter]] чтобы прочитать значение из [[Request body]]

Чтобы извлечь значение из [[URI]], Web API смотрит в [[Route data]] и в [[Query string]]. Route Data заполняется когда система маршрутизации смогла сопоставить URI и роут.

Ключевой принцип [[HTTP]] заключается в том, что ресурсы передаются в [[Request body]] с использованием [[Content negotiation]] чтобы определить [[HTTP resource representation]]

### [FromUri]
По умолчанию сложные типы читаются из [[Request body]], используя [[Media-type formatter]]. Но иногда может потребоваться преобразовать параметры из [[Query string]] в сложный тип

Например:
```csharp
http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989

public class GeoPoint
{
    public double Latitude { get; set; } 
    public double Longitude { get; set; }
}

public ValuesController : ApiController
{
    public HttpResponseMessage Get([FromUri] GeoPoint location) { ... }
}
```

Если не указать [FromUri] - то параметр `location` не заполнится, потому что Web API будет пытаться найти в экшне примитивные параметры `Latituide` и `Longitude`.

Т.е. роут должен был выглядеть так:
```csharp
public ValuesController : ApiController
{
    public HttpResponseMessage Get(double Latitude, double Longitude) { ... }
}
```

### [FromBody]

Пришло такой [[HTTP]]  сообщение:
```http
POST http://localhost:5076/api/values HTTP/1.1
User-Agent: Fiddler
Host: localhost:5076
Content-Type: application/json
Content-Length: 7

"Alice"
```

Здесь [[Request body]] - это `Alice`

Чтобы прочитать значение `Alice` нужно явно указать атрибут [FromBody]. В таком случае Web 
API смотрит в [[Content-Type header]] чтобы определить [[Media-type formatter]]. В этом примере [[Content-Type header]] это `application-json` и [[Request body]] это raw JSON string (не JSON объект).
 
Пример:
```csharp
public HttpResponseMessage Post([FromBody] string name) { ... }
```


>[!tip]- Нельзя использовать несколько [FromBody]
> В данном случае ни один из параметров не заполнится, Web API выдаст ошибку:
> `public HttpResponseMessage Post([FromBody] int id, [FromBody] string name) { ... }`
> Причина: request body might be stored in a non-buffered stream that can only be read once.
