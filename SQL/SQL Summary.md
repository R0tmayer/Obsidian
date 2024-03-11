MIN не умеет работать с NULL. Если не будет найдено ни одной записи, запрос вернёт NULL:
```sql
IIF(MIN(ContractId) = 1, 1, 0)
```
Нужно переделать на HAVING:
```sql
IF (
	EXISTS (
		SELECT
			*
			FROM table AS t 
			WHERE t.ContractId = @ContractId
			GROUP BY t.ContractId
			HAVING MIN(t.Availability) = 1
	)
)
BEGIN
	SET @Variable = 1
END
```