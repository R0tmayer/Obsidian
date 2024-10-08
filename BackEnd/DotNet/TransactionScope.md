Создаёт транзакцию в C#

```csharp
using (TransactionScope scope = new TransactionScope())
{
	// some code

	scope.Complete();
}
```

#### Complete()
Метод  проставляет флаг `_complete = true` , т.е. помечает транзакцию как выполненную, но не закрывает её.

Транзакция закрывается автоматически:
- по окончанию своего блока;
- по окончанию метода;
- при вызове scope.Dispose().

Если при закрытии транзакции флаг `_complete == false`, то будет Rollback транзакции
