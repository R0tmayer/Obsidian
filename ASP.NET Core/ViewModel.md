Используется для передачи во [[View]] более сложных структур, например:

```csharp
public class IndexViewModel
{
    public IEnumerable<Phone> Phones { get; set; }
    public IEnumerable<Company> Companies { get; set; }
}
```

```csharp
public class MyController : Controller
{
	public IActionResult Index(int? id)
	{
		var phones = new  IEnumerable<Phone>...
		var companies = new  IEnumerable<Company>...
		var model = new ProductDataViewModel { Product = product };
		return View(model);
	}
}
```
Во [[View]] потребуется указать ссылку на ViewModel
```csharp
@model ProductViewModel
```

>[!hint]- Передача простой модели
>
Если требуется передать просто модель или лист, то используй ![[ASP.NET Core#^bf109b]] ![[ASP.NET Core#^9b5e6a]]
