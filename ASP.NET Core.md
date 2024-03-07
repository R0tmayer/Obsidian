При передаче из [[Controller]] во [[View]] простой [[DomainModel]] или List<[[DomainModel]]>, достаточно просто написать:

> ProductController.cs
``` csharp
public IActionResult Index(int? id)
{
	var product = _productService.GetById(id);
	return View(product);
}
```
Тогда во [[View]] достаточно просто обратиться к Model:

> Views/Product/Index.cshtml
``` csharp
@if(Model is null)
{}
else
{
	Model.Id
	Model.Name
}
```
Если во [[View]] передаём List<[[DomainModel]]>, то аналогично:
``` csharp
@if (Model is null || Model.Count == 0)
{
    <p>No products found.</p>
}
else
{
	@foreach (var product in Model)
	{
		product.Id
		product.Name
	}
}

