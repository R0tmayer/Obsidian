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
		var phones = new IEnumerable<Phone>...
		var companies = new IEnumerable<Company>...
		var model = new MyViewModel { Phones = phone, Companies = companies };
		return View(model);
	}
}
```
Во [[View]] потребуется указать ссылку на MyViewModel
```csharp
@model IndexViewModel

@ if (Model.Phones ... Model.Companies)
```

> [!note]- Передача простой модели
> Если требуется передать просто модель или List (без ViewModel):
> ``` csharp
> public IActionResult Index(int? id)
> {
> 	var product = _productService.GetById(id);
> 	return View(product);
> }
> ```
> ```csharp
> @if(Model is null)
> {}
> else
> {
> 	Model.Id
> 	Model.Name
> }
> ```

