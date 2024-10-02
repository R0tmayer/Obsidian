Создаёт транзакцию в C#

```csharp
using (TransactionScope scope = new TransactionScope())
{
	// some code

	scope.Complete();
}
```

#### Complete()
Метод `помечает` транзакцию как выполненную, но не закрывает её. Транзакция закрывается автоматически по окончанию своего блока или по окончанию метода или если вызвать scope.Dispose()

Если при закрытии 
