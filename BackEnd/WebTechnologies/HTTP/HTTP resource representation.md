Например клиент делает GET запрос `/programmers/Namespacinator` и получает JSON ответ: ^60a941
```json
{ 
	"nickname": "Namespacinator", 
	"powerLevel": 5 
}
```

Это не [[HTTP Resource]]. Это representation (представление) программного ресурса. Сейчас это в JSON виде, но сервер мог представить ответ в формате XML, HTML и т.д.