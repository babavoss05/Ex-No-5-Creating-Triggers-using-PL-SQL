# Ex. No: 5 Creating Triggers using PL/SQL

### AIM: To create a Trigger using PL/SQL.

### Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
3. Create a trigger named as log_salary-update.
4. Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
5. End the trigger.
6. Update the salary of an employee in employee table.
7. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
8. Display the employee table, salary_log table.

### Program:
### Create employee table:
```sql
create table employee(empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
insert into employee values(1,'Sita','HR',70000);
insert into employee values(2,'Anjali','MD',95000);
insert into employee values(3,'Chandhini','Finance',80000);
```

### Create salary_log table:
```sql
create table salary_log (log_id NUMBER , empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
```

### PLSQL Trigger code:
```sql
create or replace trigger log_salary_update
before update on employee
for each row
declare
v_old_salary number;
v_new_salary number;
begin
v_old_salary := :OLD.salary;
v_new_salary := :NEW.salary;
if v_old_salary <> v_new_salary then
insert into salary_log(empid,empname,old_salary,new_salary,update_date)
values(:OLD.empid,:OLD.empname,v_old_salary,v_new_salary,SYSDATE);
end if;
end;
/
```
### Update the salary of an employee:
``` sql
update employee set salary = 97000 where empid = 2;
```
### Display the salary log table:
```sql
select * from salary_log;
```
### Output:
![image](https://github.com/dineshgl/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/103019882/96cf1364-513a-4a70-ad0d-e9981288b432)


### Result:
Thus a trigger using PL/SQL is created successfully.
