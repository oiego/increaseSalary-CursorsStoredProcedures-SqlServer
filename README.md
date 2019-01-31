
drop procedure increaseSalary
go
/**-- procedimiento que incremente sueldo de los empleados considerando las sig reglas:*/
create procedure increaseSalary
AS
declare @sal INT,
		@id varchar(5)
declare c1 cursor for select StaffNo from staff;
open c1
fetch next from c1 into @id 
while @@FETCH_STATUS = 0 begin
    set @sal = (select salary from staff where StaffNo = @id)
	if @sal >= 20000
		set @sal = @sal*1.1
	else if (@sal >= 10000 and @sal < 20000)
		set @sal = @sal*1.15
	else 
		set @sal = 10000
	update staff set salary = @sal where staffNo = @id
	fetch c1 into @id
	end
close c1
DEALlOCATE C1
