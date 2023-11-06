# Ex-No-5-Creating-Triggers-using-PL-SQL
## DATE:19/09/23
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
```-- Create the employee table
CREATE TABLE employed(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);

CREATE TABLE sal_log (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
-- Insert the values in the employee table
insert into employed values(1,'Shakthi','IT',1000000);
insert into employed values(2,'Suju','SALES',500000)

```
### Create employee table
![Screenshot 2023-10-06 161851](https://github.com/DEVADARSHAN2/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119432150/de7d8326-7017-44f2-bea8-421c4b85b265)

### Create salary_log table
![Screenshot 2023-10-06 161903](https://github.com/DEVADARSHAN2/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119432150/121c6f37-808d-495e-a219-74ede0299f5a)

### PLSQL Trigger code
```
-- Create the trigger
CREATE OR REPLACE TRIGGER log_sal_update
BEFORE UPDATE ON employed
FOR EACH ROW
BEGIN
  IF :OLD.salary != :NEW.salary THEN
    INSERT INTO sal_log (empid, empname, old_salary, new_salary, update_date)
    VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  END IF;
END;
/
-- Insert the values in the employee table
insert into employed values(1,'Shakthi','IT',1000000);
insert into employed values(2,'Suju','SALES',500000);

-- Update the salary of an employee
UPDATE employed
SET salary = 60000
WHERE empid = 1;
-- Display the employee table
SELECT * FROM employed;

-- Display the salary_log table
SELECT * FROM sal_log;
```

### Output:
![Screenshot 2023-10-06 161911](https://github.com/DEVADARSHAN2/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119432150/5dcb3a74-e455-4418-bc6c-9e006a3cca4d)


### Result:
 The program has been implemented successfully
