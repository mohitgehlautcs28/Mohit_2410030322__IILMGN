# EXPERIMENT10
#### QUERY 1: Display the names of employees from department number 10 with salary greater than that of any employee working in other departments.
```sql
 SELECT ename from employee WHERE deptno = 10 AND
sal > (select MIN(sal) from employee WHERE deptno <> 10);

 SELECT ename from employee WHERE deptno = 10 AND
 sal > ANY(select sal from employee WHERE deptno <> 10
 
 +--------+
| ename  |
+--------+
| MILLER |
+--------+
1 row in set (0.064 sec)
```

#### QUERY 2: Display the names of employee from department number 10 with salary greater than that of all employee working in other departments.
```sql
 SELECT ename from employee WHERE deptno = 10 AND
 sal > ALL(select sal from employee WHERE deptno <> 10);

 SELECT ename from employee WHERE deptno = 10 AND
 sal  > (select MAX(sal) from employee WHERE deptno <> 10);
 
 Empty set (0.001 sec)
 ```
 #### QUERY 3: Display the details of employees who are in sales dept and grade is 3.
 ```sql
 SELECT E.ENAME,D.DNAME,E.JOB,E.SAL,E.EMPNO,D.DEPTNO FROM EMPLOYEE E
 JOIN DEPARTMENT D ON E.DEPTNO  = D.DEPTNO JOIN SALGRADE S ON E.SAL BETWEEN S.LOWSAL
 AND S.HIGHSAL WHERE D.DNAME = 'SALES' AND S.GRADE = 3;
 
 +--------+-------+----------+------+-------+--------+
| ENAME  | DNAME | JOB      | SAL  | EMPNO | DEPTNO |
+--------+-------+----------+------+-------+--------+
| ALLEN  | sales | SALESMAN | 1600 |  7499 |     30 |
| TURNER | sales | SALESMAN | 1650 |  7844 |     30 |
+--------+-------+----------+------+-------+--------+
2 rows in set (0.002 sec)
```
  #### QUERY 4: Display those who are not managers and who are managers anyone. 
  ```sql
select ename from employee where empno
  IN (select mgr from employee);
  
  +-------+
| ename |
+-------+
| JONES |
| BLAKE |
| CLARK |
| SCOTT |
| KING  |
| FORD  |
+-------+
6 rows in set (0.003 sec)
   PART 2:
  select ename from employee where empno
  NOT IN (select mgr from employee WHERE mgr IS NOT NULL);
  
  +--------+
| ename  |
+--------+
| SMITH  |
| ALLEN  |
| WARD   |
| MARTIN |
| TURNER |
| ADAMS  |
| JAMES  |
| MILLER |
+--------+
8 rows in set (0.003 sec)
```
  #### QUERY 5: Display those employees whose manager name is jones. 
  ```sql
  SELECT enameFROM employee
  WHERE mgr = ( SELECT empno FROM employee WHERE ename = 'JONES');
  
  +-------+
| ename |
+-------+
| SCOTT |
| FORD  |
+-------+
2 rows in set (0.002 sec)
```
  #### QUERY 6: Display ename who are working in sales dept.
   ```sql
select ename from  employee WHERE deptno =(select
   deptno from department WHERE dname ='sales');
   
   +--------+
| ename  |
+--------+
| ALLEN  |
| WARD   |
| MARTIN |
| BLAKE  |
| TURNER |
| JAMES  |
+--------+
6 rows in set (0.001 sec)
```
  #### QUERY 7: Display employee name, deptname, salary and comm. For those sal in between 2000 to 5000 while location is chicago.
   ```sql
SELECT e.ename, d.dname, e.sal, e.compp FROM employee e
   JOIN Department d ON e.deptno = d.deptno
    WHERE e.sal BETWEEN 2000 AND 5000
    AND d.location = 'FRANCE';
    
    +-------+------------+------+-------+
| ename | dname      | sal  | compp |
+-------+------------+------+-------+
| JONES | accounting | 3273 |  NULL |
| CLARK | accounting | 2695 |  NULL |
| FORD  | accounting | 3300 |  NULL |
+-------+------------+------+-------+
3 rows in set (0.002 sec)
```
   #### QUERY 8: Display those employees whose salary greater than his manager salary. 
   ```sql
SELECT e.ename, e.sal, m.ename AS manager_name, m.sal AS manager_sal
   FROM employee e
   JOIN employee m ON e.mgr = m.empno
   WHERE e.sal > m.sal;
   
   +-------+------+--------------+-------------+
| ename | sal  | manager_name | manager_sal |
+-------+------+--------------+-------------+
| SCOTT | 3300 | JONES        |        3273 |
| FORD  | 3300 | JONES        |        3273 |
+-------+------+--------------+-------------+
2 rows in set (0.002 sec)
```
  #### QUERY 9: Display those employees who are working in the same dept where his manager is working.
  ```sql
SELECT e.ename, e.deptno, m.ename AS manager_name, m.deptno AS manager_dept
  FROM employee e
  JOIN employee m ON e.mgr = m.empno
   WHERE e.deptno = m.deptno;
   
   +--------+--------+--------------+--------------+
| ename  | deptno | manager_name | manager_dept |
+--------+--------+--------------+--------------+
| SMITH  |     20 | FORD         |           20 |
| ALLEN  |     30 | BLAKE        |           30 |
| WARD   |     30 | BLAKE        |           30 |
| JONES  |     20 | KING         |           20 |
| MARTIN |     30 | BLAKE        |           30 |
| CLARK  |     20 | KING         |           20 |
| TURNER |     30 | BLAKE        |           30 |
| JAMES  |     30 | BLAKE        |           30 |
| FORD   |     20 | JONES        |           20 |
+--------+--------+--------------+--------------+
9 rows in set (0.001 sec)
```
  #### QUERY 10: Display grade and employees name for the dept no 10 or 30 but grade is not 4, while joined the company before 31-dec-82.
  ```sql
select e.ename,s.grade from employee e
   join salgrade s on e.sal between s.lowsal and s.highsal
   where e.deptno not in (10,20)
   and s.grade <> 4
   and e.hiredate < '1982-12-31';
   
+--------+-------+
| ename  | grade |
+--------+-------+
| ALLEN  |     3 |
| WARD   |     2 |
| MARTIN |     2 |
| BLAKE  |     5 |
| SCOTT  |     5 |
| TURNER |     3 |
| JAMES  |     1 |
+--------+-------+
7 rows in set (0.002 sec)
```
