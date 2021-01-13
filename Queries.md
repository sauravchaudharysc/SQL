### 1.  Perform the given queries?

**i .** Find the second highest salary of an employee ?
**ii .** Find the third highest salary of an employee ?
**iii .** List the person Emp_No with third highest salary? 
**iii .**Find the second minimum salary of an employee?

| EMP_NO | SAL  |
| ------ | ---- |
| 7839   | 5000 |
| 7698   | 2000 |
| 7782   | 4000 |
| 7566   | 4000 |
| 7788   | 3000 |
| 7369   | 1000 |
| 7902   | 3000 |

**Ans :**
**Create & Insert**

```sql
Create Table Employee(
 Emp_No INT,
 SAL INT
 );
```

```sql
Insert INTO Employee 
Values (7839,5000);
Insert INTO Employee 
Values (7698,2000);
Insert INTO Employee 
Values (7782,4000);
Insert INTO Employee 
Values (7566,4000);
Insert INTO Employee 
Values (7788,3000);
Insert INTO Employee 
Values (7369,1000);
Insert INTO Employee 
Values (7902,3000);
```

**i.**

```sql
Select Max(SAL) From Employee
Where SAL NOT IN(Select Max(SAL) From Employee);

--Or
Select Max(SAL) From Employee
Where SAL < (Select Max(SAL) From Employee);
```

**ii.**

```sql
Select distinct(Emp1.Sal) as Salary 
From Employee Emp1 where 
2 = (select(count(distinct(Emp2.sal))) from 
Employee Emp2 where 
Emp2.sal>Emp1.sal);
```

**iii.**

```sql
Select distinct(Emp1.Sal),Emp1.Emp_No as Emp_No 
From Employee Emp1 where 
2 = (select(count(distinct(Emp2.sal))) from 
Employee Emp2 where 
Emp2.sal>Emp1.sal);
```

**iv.**

```sql
Select Emp1.Sal as Salary,Emp1.Emp_No as Emp_No  
From Employee Emp1 where  
1 = (select(count(distinct(Emp2.sal))) from  
Employee Emp2 where  
Emp1.sal>Emp2.sal)
```

### 2. Perform the given Queries 

| DEPT_NO | SAL  | ENAME |
| ------- | ---- | ----- |
| 30      | 4000 | BLAKE |
| 10      | 2000 | CLARK |
| 20      | 2000 | JONES |
| 20      | 3000 | SCOTT |
| 20      | 3000 | FORD  |
| 20      | 1000 | SMITH |
| 10      | 5000 | KING  |

**i .** Maximum Salary Department Wise ?
**ii .** Minimum Salary Department Wise ?
**ii .** No of people in each department ?
**iii.** Name the employee who have highest salary in thier respective department ?

**Ans :**
**Create & Insert**

```sql
CREATE TABLE EMPLOYEES(
    DEPT_NO INT,
    SAL INT,
    ENAME VARCHAR(255)
);
```

```sql
INSERT INTO EMPLOYEES
VALUES (10,5000,'KING');
INSERT INTO EMPLOYEES
VALUES (30,4000,'BLAKE');
INSERT INTO EMPLOYEES
VALUES (10,2000,'CLARK');
INSERT INTO EMPLOYEES
VALUES (20,2000,'JONES');
INSERT INTO EMPLOYEES
VALUES (20,3000,'SCOTT');
INSERT INTO EMPLOYEES
VALUES (20,3000,'FORD');
INSERT INTO EMPLOYEES
VALUES (20,1000,'SMITH');
```

```sql
--i
SELECT MAX(SAL),DEPT_NO FROM EMPLOYEES
GROUP BY DEPT_NO;

--ii
SELECT MIN(SAL),DEPT_NO FROM EMPLOYEES
GROUP BY DEPT_NO;

--iii
SELECT COUNT(*),DEPT_NO FROM EMPLOYEES
GROUP BY DEPT_NO;

--iv
Select * From Employees Where
Sal In(
SELECT MAX(SAL) FROM EMPLOYEES
GROUP BY DEPT_NO)
Order By Dept_No;
```

### 3. Perform the given Queries on the given table in Q no 2

**i.** Print the tuples at odd position ?
**ii.** Print the tuples at even position ? 

```sql
--i.
Select * From (
Select rownum as No ,Dept_No,Sal as Salary,Ename as Name From Employees
)where mod(No,2)<>0;

--ii.
Select * From (
Select rownum as No ,Dept_No,Sal as Salary,Ename as Name From Employees
)where mod(No,2)=0;


```

### 3. List those ename whose frequency >1**

| ENAME |
| :---: |
| TRISH |
| TRISH |
| RISHI |
| RISHI |
| TRISH |
| FORD  |
| SMITH |

**Create & Insert**

```
CREATE TABLE EMP(
   
    ENAME VARCHAR(255)
);

INSERT INTO EMP
VALUES ('TRISH');

INSERT INTO EMP
VALUES ('TRISH');

INSERT INTO EMP
VALUES ('RISHI');

INSERT INTO EMP
VALUES ('RISHI');

INSERT INTO EMP
VALUES ('TRISH');

INSERT INTO EMP
VALUES ('FORD');

INSERT INTO EMP
VALUES ('SMITH');
```

**Ans :**

```sql
Select * From Emp
Group By Ename
Having Count(*)>1;
```

> **NOTE:** All rows cant be printed using * operator. We need to specify column name.



**4.** Find the Pattern

|  NAME  |
| :----: |
|  KING  |
| BLAKE  |
| CLARK  |
| JONES  |
| SCOTT  |
|  FORD  |
| SMITH  |
| Allen  |
|  Ward  |
| Martin |
| Turner |
| Adams  |
| James  |
| Miller |

**Create & Insert**

```sql
Create Table Name(
    Name varchar(255)
);

Insert Into Name 
Values('KING');
Insert Into Name 
Values('BLAKE');
Insert Into Name 
Values('CLARK');
Insert Into Name 
Values('JONES');
Insert Into Name 
Values('SCOTT');
Insert Into Name 
Values('FORD');
Insert Into Name 
Values('SMITH');
Insert Into Name 
Values('Allen');
Insert Into Name 
Values('Ward');
Insert Into Name 
Values('Martin');
Insert Into Name 
Values('Turner');
Insert Into Name 
Values('Adams');
Insert Into Name 
Values('James');
Insert Into Name 
Values('Miller');
```

**Note :** Be careful for case . 

**Ans:**

```sql

--Start with M
Select * From Name
Where Name like 'M%';

--Ends with n
Select * From Name
Where Name like '%n';

--Having m at any position
Select * From Name
Where Name like '%m%';

--No m & M at any position
Select * From Name
Where (Name NOT like '%m%' AND  Name NOT like '%M%');

--Having 2 continous ll at any position
Select * From Name
Where Name like '%ll%';

--Having l at second place
Select * From Name
Where Name like '_l%';

--Any Value that Starts With A and is of Length 5
Select * From Name
Where Name like '_l%';

--Any Value that end with e
Select * From Name
Where Name like '%e_';
```

### 5. Union & Union All

**Sample1**

| CITY      | COUNTRY |
| --------- | ------- |
| hyderabad | india   |
| london    | uk      |
| texas     | usa     |

**Sample2**

| CITY      | COUNTRY |
| --------- | ------- |
| hyderabad | india   |
| hyderabad | india   |
| hyderabad | india   |
| bhutan    | thimpu  |

**Union**

```sql
select city,country from sample2
union
select city,country from sample1
```

|   CITY    | COUNTRY |
| :-------: | :-----: |
|  bhutan   | thimpu  |
| hyderabad |  india  |
|  london   |   uk    |
|   texas   |   usa   |

**Union All**

```sql
select city,country from sample2
union all
select city,country from sample1
```

| CITY      | COUNTRY |
| --------- | ------- |
| hyderabad | india   |
| london    | uk      |
| texas     | usa     |
| hyderabad | india   |
| hyderabad | india   |
| hyderabad | india   |
| bhutan    | thimpu  |

### 6. Joins

**Employee**

| EMPNO | ENAME | JOB       | MGR  | HIREDATE  | SAL  | COMM | DEPTNO |
| ----- | ----- | --------- | ---- | --------- | ---- | ---- | ------ |
| 7839  | KING  | PRESIDENT | -    | 17-NOV-81 | 5000 | -    | 10     |
| 7698  | BLACK | MANAGER   | 7839 | 01-MAY-81 | 2850 | -    | 30     |
| 7782  | CLARK | MANAGER   | 7839 | 09-JUN-81 | 2450 | -    | 10     |
| 7566  | JONES | MANAGER   | 7839 | 02-APR-81 | 2975 | -    | 20     |
| 7788  | SCOTT | ANALYST   | 7566 | 19-APR-87 | 3000 | -    | 20     |
| 7902  | FORD  | ANALYST   | 7566 | 03-DEC-81 | 3000 | -    | 20     |
| 7369  | SMITH | CLERK     | 7902 | 17-DEC-80 | 800  | -    | 20     |

**Department**

| DEPTNO | DNAME      | LOC      |
| ------ | ---------- | -------- |
| 10     | ACCOUNTING | NEW YORK |
| 20     | RESEARCH   | DALLAS   |
| 30     | SALES      | CHICAGO  |
| 40     | OPERATIONS | BOSTON   |

**Create & Insert**

```sql
Create Table Employee(
    EMPNO int PRIMARY KEY,
    ENAME VARCHAR(255),
    JOB VARCHAR(255),
    MGR INT,
    HIREDATE Date,
    SAL INT,
    COMM varchar(255),
    DEPTNO int
);

insert into Employee
values(7839,'KING','PRESIDENT',null,TO_DATE('17/11/1981' , 'dd/mm/yyyy'),5000,null,10);
insert into Employee
values(7698,'BLACK','MANAGER',7839,TO_DATE('01/05/1981' , 'dd/mm/yyyy'),2850,null,30);
insert into Employee
values(7782,'CLARK','MANAGER',7839,TO_DATE('09/06/1981' , 'dd/mm/yyyy'),2450,null,10);
insert into Employee
values(7566,'JONES','MANAGER',7839,TO_DATE('02/04/1981' , 'dd/mm/yyyy'),2975,null,20);
insert into Employee
values(7788,'SCOTT','ANALYST',7566,TO_DATE('19/04/1987' , 'dd/mm/yyyy'),3000,null,20);
insert into Employee
values(7902,'FORD','ANALYST',7566,TO_DATE('03/12/1981' , 'dd/mm/yyyy'),3000,null,20);
insert into Employee
values(7369,'SMITH','CLERK',7902,TO_DATE('17/12/1980' , 'dd/mm/yyyy'),800,null,20);

create table dept(
    DEPTNO INT PRIMARY KEY,
    DNAME VARCHAR(255),
    LOC VARCHAR(255)
);


INSERT INTO DEPT
VALUES(10,'ACCOUNTING','NEW YORK');

INSERT INTO DEPT
VALUES(20,'RESEARCH','DALLAS');

INSERT INTO DEPT
VALUES(30,'SALES','CHICAGO');

INSERT INTO DEPT
VALUES(40,'OPERATIONS','BOSTON');
```

Ans :

```sql
--Details of Employee
select ename,sal,dept.deptno,dname,loc
from employee emp,dept
where emp.deptno=dept.deptno;

--Details of Employee who lives in chicago
select ename,sal,dept.deptno,dname,loc
from employee emp,dept
where emp.deptno=dept.deptno and loc='CHICAGO';

--Sum of salary of each department
select dname,sum(sal)
from employee emp,dept
where emp.deptno=dept.deptno
group by dname;

--Name of the manager of employee
select e1.ename as Employee , e2.ename as Manager
from employee e1,employee e2
where e2.empno=e1.mgr;

--Name of employee whose salary is more than manager
select e1.ename as Employee , e2.ename as Manager
from employee e1,employee e2
where e2.empno=e1.mgr and e1.sal>e2.sal;

--Left Join
select rownum,EmpNo,Ename,Emp.DeptNo,Dname,Loc,Job
from Employee Emp
Left Join
Dept
on Emp.deptno=Dept.deptno;

--Left join but dname='SALES'
select rownum,EmpNo,Ename,Emp.DeptNo,Dname,Loc,Job
from Employee Emp
Left Join
Dept
on Emp.deptno=Dept.deptno and dname='SALES';

--Right Join
select rownum,EmpNo,Ename,Emp.DeptNo,Dname,Loc,Job
from Employee Emp
Right Join
Dept
on Emp.deptno=Dept.deptno ;

--full join
select rownum,EmpNo,Ename,Emp.DeptNo,Dname,Loc,Job
from Employee Emp
Full Join
Dept
on Emp.deptno=Dept.deptno ;

--cross join
select rownum,EmpNo,Ename,Emp.DeptNo,Dname,Loc,Job
from Employee Emp
cross join
Dept

```

### 7. Perform given Queries on Table of Qno 6

**1. Display first and last row of table.**

> **Note:** rownum can be only used with less than operator.

```sql
select * from (select rownum r,ename from employee)
where r=1 or r=(select count(*) from employee);
```

**2. Display last two row of table.**

```sql
--Display Last Two Rows Of Table
select * from (select rownum r,ename from employee)
where r=(select count(*)-1 from employee) or r=(select count(*) from employee);
```

**3. Display First and Last two row of table.**

```sql
select * from (select rownum r,ename from employee)
where r=1 or r=(select count(*)-1 from employee) or r=(select count(*) from employee);
```

### 8. 2nd Lowest Salary From Employee

```sql
Select emp1.Sal from
Employee emp1
where 1 = (Select count(distinct(emp2.Sal)) from Employee emp2
where emp2.Sal<emp1.sal) ;
```

### 9. Nth Lowest Salary From Employee

```sql
Select * from (select distinct sal from Employee 
Order By SAL DESC)
where rownum<=3;
```

