Родительский элемент всех [[Collections]] в DotNet.

Используется для ленивой загрузки данных.

Рассмотрим следующий код:

```csharp
using (var dbContext = new MyDbContext())
{
    IEnumerable<Product> products = dbContext.Products;

    foreach (var product in products)
    {
        Console.WriteLine($"Name: {product.Name}, Price: {product.Price}");
    }
}
```

^c94fbc

Содержимое переменной ``products``:

- ``Current``: текущий элемент выборки;
- ``GetEnumerator()``: возвращает объект типа [[IEnumerator]] с помощью которого осуществляется итерация по выборке;

Под капотом происходит примерно следующее:
```csharp
IEnumerable<Product> products = dbContext.Products;
IEnumerator<Product> enumerator = products.GetEnumerator();

while (enumerator.MoveNext())
{
    Product currentProduct = enumerator.Current;
    Console.WriteLine($"Name: {currentProduct.Name}, Price: {currentProduct.Price}");
}

enumerator.Dispose();
```

Таким образом в ``products`` не хранится вся выборка продуктов из БД. <u>То есть сама выборка хранится в памяти БД</u>. Вместо этого переменная хранит информацию о том, как нужно обойти выборку. 


Рассмотрим другой пример код:
```csharp
public IEnumerable<string> GetData()  
{  
	yield return "Data 1";  
	yield return "Data 2";  
	yield return "Data 3";  
}

public void MyMethod()  
{  
	IEnumerable<string> data = GetData();  
	ProcessData(data);  
	ProcessData(data);  
}
```
При создании ``data`` еще не загружаются фактические элементы, а создается объект, который знает, как получить элементы по мере необходимости. Т.е. ``data`` как некий делегат, хранит в себе ссылку на ``GetData()``, а если быть точнее то информацию о способе получения элементов при обращении к ним. Таким образом <u>обращаясь к ``data`` будет вызван метод ``GetData()``. В итоге метод ``GetData()`` будет вызван 3 раза. </u>

Если нужно перебрать коллекцию и сразу сохранить её в память приложения, то:

```csharp
IEnumerable<string> dataList = GetData().ToList();
IEnumerable<string> dataArray = GetData().ToArray();  
```

В данном коде [[IEnumerable#^c94fbc]]  при вызове ``dbContext.Products`` на стороне БД будет вызван запрос и данные будет храниться в БД, а не в приложении. 
```sql
SELECT [Id], [Name], [Price]
FROM [Products]
```
После чего итерируясь в цикле элементы из выборки достаются по одному:
```csharp
foreach (var product in products)
{
	Console.WriteLine($"Name: {product.Name}, Price: {product.Price}");
}
```




