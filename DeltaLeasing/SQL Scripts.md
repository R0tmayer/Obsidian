- Выдача права сотруднику (сейчас на тестовом не работает страница)

> [!note]- ВЫДАЧА ПРАВА
> 
> ```sql
> DECLARE 
> 	@EmployeeId int = 1807,
> 	@RequesterId int = 2311,
> 	@RightId int = 759,
> 	@IncidentId int = 247408
> 
> INSERT INTO rights.RightsChangeLog (EmployeeId, RequesterId, RightId, CenterCodeId, IsGranted, IncidentId, ValidFrom, ValidTo)
>     VALUES (@EmployeeId, @RequesterId, @RightId, NULL, 1, @IncidentId, GETDATE(), NULL)
> 
> DECLARE @ChangeLogId int = SCOPE_IDENTITY()
> 
> 
> DROP TRIGGER [rights].[ChangelogUpdate]
> 
> 
> EXEC rights.EmpApproveRightChange
>     @RightsChangeLogId = @ChangeLogId,
>     @EditorId = 69 --- Admin
> ```