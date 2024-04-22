Например клиент делает GET запрос `/programmers/Namespacinator` и получает JSON ответ:
```json
{ 
	"nickname": "Namespacinator", 
	"powerLevel": 5 
}
```

Это не программный ресурс. Это representation (представление) программного ресурса. Сейчас это в JSON виде, но сервер мог представить ответ в формате XML, HTML и т.д.