Иногда когда на входе в процедуру передаются динамические параметры, например разные операторы (>, <, IS NULL, IS NOT NULL, etc.), то можно в рантайме подставлять эти значения.

Пример кода:
```sql
CREATE PROCEDURE GetReportData
  @Parameter int,
  @Operator varchar(10),
  @ValueToCompare int
AS
BEGIN
    DECLARE @SQL nvarchar(max) = '
        SELECT *
        FROM ReportData
        WHERE @Parameter @Operator @ValueToCompare'

  SET @SQL = REPLACE(@SQL, '@Parameter', @Parameter)
  SET @SQL = REPLACE(@SQL, '@Operator', @Operator)
  SET @SQL = REPLACE(@SQL, '@ValueToCompare', @ValueToCompare)

  EXEC sp_executesql @SQL
END
```

Ещё лучше, когда вызываешь процедуру `sp_executesql`, то вместо Replace вставлять параметры как в процедуре через запятую. чтобы сверялись типы и это более производительнее:
```sql
EXEC sp_executesql @SQL, @Parameter, @Operator, @ValueToCompare
```
