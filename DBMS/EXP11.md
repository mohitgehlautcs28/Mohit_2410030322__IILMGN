# EXPERIMENT 11
#### QUERY 1: Delete those employees who joined the company before 31dec-82 while there dept location is ‘new york’ or ‘france’. 
```sql
 DELETE FROM employee
    -> WHERE hiredate < '1982-12-31'
    ->   AND deptno IN (
    ->     SELECT deptno FROM department
    ->     WHERE location IN ('NEW YORK','FRANCE')
    ->   );
Query OK, 6 rows affected (0.009 sec)
```
#### QUERY 2: Display employee name, job, deptname, location for all who are working as managers.  
```sql
SELECT e.ename, e.job, d.dname, d.location
    -> FROM employee e
    -> JOIN department d ON e.deptno = d.deptno
    -> WHERE e.job = 'MANAGER';
+-------+---------+-------+------------+
| ename | job     | dname | location   |
+-------+---------+-------+------------+
| BLAKE | MANAGER | sales | LOS ANGLES |
+-------+---------+-------+------------+
1 row in set (0.001 sec)
```
#### QUERY 3: Display name and salary of ford if his sal is equal to high sal of his grade. 
```sql
 SELECT ename, sal
    -> FROM employee e
    -> JOIN salgrade s ON e.sal BETWEEN s.lowsal AND s.highsal
    -> WHERE e.ename = 'FORD'
    ->   AND e.sal = s.highsal;
Empty set (0.001 sec)
```
#### QUERY 4: Find out the top 5 earner of company. 
```sql
 SELECT ename, sal
    -> FROM employee
    -> ORDER BY sal DESC
    -> LIMIT 5;
+--------+------+
| ename  | sal  |
+--------+------+
| SCOTT  | 3300 |
| BLAKE  | 3135 |
| TURNER | 1650 |
| ALLEN  | 1600 |
| MARTIN | 1250 |
+--------+------+
5 rows in set (0.002 sec)
```
#### QUERY 5: Display the name of those employees who are getting highest salary.  
```sql
SELECT ename
    -> FROM employee
    -> WHERE sal = (SELECT MAX(sal) FROM employee);
+-------+
| ename |
+-------+
| SCOTT |
+-------+
1 row in set (0.001 sec)
```
#### QUERY 6: Display those employees whose salary is equal to average of maximum and minimum. 
```sql
SELECT ename
    -> FROM employee
    -> WHERE sal = (
    ->   (SELECT (MAX(sal) + MIN(sal)) / 2
    ->    FROM employee)
    -> );
Empty set (0.001 sec)
```
#### QUERY 7: Display dname where at least 3 are working and display only dname. 
```sql
 SELECT d.dname
    -> FROM department d
    -> WHERE (SELECT COUNT(*) FROM employee e WHERE e.deptno = d.deptno) >= 3;
+-------+
| dname |
+-------+
| sales |
+-------+
1 row in set (0.002 sec)
```
#### QUERY 8: Display name of those managers names whose salary is more than average salary of company.
```sql
SELECT ename
    -> FROM employee
    -> WHERE job = 'MANAGER'
    ->   AND sal > (SELECT AVG(sal) FROM employee);
+-------+
| ename |
+-------+
| BLAKE |
+-------+
1 row in set (0.001 sec)
```
#### QUERY 9: Display those managers name whose salary is more than an average salary of his employees. 
```sql
SELECT m.ename
    -> FROM employee m
    -> WHERE m.job = 'MANAGER'
    ->   AND m.sal > (
    ->     SELECT AVG(e.sal)
    ->     FROM employee e
    ->     WHERE e.mgr = m.empno
    ->   );
+-------+
| ename |
+-------+
| BLAKE |
+-------+
1 row in set (0.001 sec)
```
#### QUERY 10: Display employee name, sal, comm and net pay for those employees whose net pay are greater than or equal to any other employee salary of the company? 
```sql
 SELECT ename, sal, compp, (sal + IFNULL(compp,0)) AS netpay
    -> FROM employee
    -> WHERE (sal + IFNULL(compp,0)) >= ANY (SELECT sal FROM employee);
+--------+------+-------+--------+
| ename  | sal  | compp | netpay |
+--------+------+-------+--------+
| ALLEN  | 1600 |   300 |   1900 |
| WARD   | 1250 |   300 |   1550 |
| MARTIN | 1250 |  1400 |   2650 |
| BLAKE  | 3135 |  NULL |   3135 |
| SCOTT  | 3300 |  NULL |   3300 |
| TURNER | 1650 |     0 |   1650 |
| ADAMS  | 1210 |  NULL |   1210 |
| JAMES  | 1045 |  NULL |   1045 |
+--------+------+-------+--------+
8 rows in set (0.002 sec)
```
