Если ContractId = NULL, то код вернёт NULL
```sql
IIF(MIN(ContractId) = 1, 1, 0)
```
Нужно переделать на Exists