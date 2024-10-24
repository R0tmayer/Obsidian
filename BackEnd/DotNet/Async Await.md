Здесь три таски запустятся одновременно. Start() запускает логику таски. А await - мы просто забираем результат.
```csharp
Task firstTask = new Task(() => Console.WriteLine("firstTask"));
Task secondTask = new Task(() => Console.WriteLine("secondTask"))
Task thirdTask = new Task(() => Console.WriteLine("thirdTask"))		

firstTask.Start();
secondTask.Start();
thirdTask.Start();

var firstResult = await firstTask;
var secondResult = await secondTask;
var thirdResult = await thirdTask;
```