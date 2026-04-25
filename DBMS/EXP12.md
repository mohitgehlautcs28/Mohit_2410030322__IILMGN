# EXPERIMENT 12
#### QUERY 1 : Display those employees whose salary is less than his manager but more than salary of any other managers. 
```sql
SELECT e.ename
    -> FROM employee e
    -> JOIN employee m ON e.mgr = m.empno
    -> WHERE e.sal < m.sal
    ->   AND e.sal > ANY (SELECT sal FROM employee WHERE job = 'MANAGER');
+-------+
| ename |
+-------+
| JONES |
| BLAKE |
+-------+
2 rows in set (0.002 sec)
```
#### QUERY 2 : Find out the number of employees whose salary is greater than their manager salary? 
```sql
 SELECT COUNT(*) FROM EMPLOYEE e JOIN EMPLOYEE m ON
    -> e.mgr = m.empno WHERE e.sal > m.sal;
+----------+
| COUNT(*) |
+----------+
|        2 |
+----------+
1 row in set (0.003 sec)
```
#### QUERY 3 : Display those managers who are not working under president but they are working under any other manager? 
```sql
SELECT ename FROM employee e WHERE job = 'MANAGER'
    -> AND mgr NOT IN (SELECT empno from employee WHERE job = 'PRESIDENT')
    -> AND mgr is NOT NULL;
Empty set (0.006 sec)
```
#### QUERY 4 : Delete those department where no employee working? 
```sql
DELETE FROM DEPARTMENT
    -> WHERE DEPTNO NOT IN (
    -> SELECT DEPTNO FROM EMPLOYEE WHERE DEPTNO IS NOT NULL);
Query OK, 0 rows affected (0.002 sec)
```
#### QUERY 5 : Delete those records from emp table whose deptno not available in dept table? 
```sql
DELETE FROM EMPLOYEE WHERE DEPTNO NOT IN
    -> (SELECT DEPTNO FROM DEPARTMENT);
Query OK, 0 rows affected (0.001 sec)
```
#### QUERY 6 : Display those earners whose salary is out of the grade available in sal grade table? 
```sql
SELECT ename FROM employee WHERE sal <
    -> (select min(lowsal) from salgrade) OR sal >
    -> (select max(highsal) from salgrade);
Empty set (0.009 sec)
```
#### QUERY 7 : Display employee name, sal, comm. And whose net pay is greater than any other in the company? 
```sql
SELECT ename, sal, compp, (sal + NVL(compp,0)) AS netpay
    -> FROM employee
    -> WHERE (sal + NVL(compp,0)) > ANY (SELECT sal FROM employee);
+--------+------+-------+--------+
| ename  | sal  | compp | netpay |
+--------+------+-------+--------+
| ALLEN  | 1600 |   300 |   1900 |
| WARD   | 1250 |   300 |   1550 |
| JONES  | 3273 |  NULL |   3273 |
| MARTIN | 1250 |  1400 |   2650 |
| BLAKE  | 3135 |  NULL |   3135 |
| CLARK  | 2695 |  NULL |   2695 |
| SCOTT  | 3300 |  NULL |   3300 |
| KING   | 5500 |  NULL |   5500 |
| TURNER | 1650 |     0 |   1650 |
| ADAMS  | 1210 |  NULL |   1210 |
| JAMES  | 1045 |  NULL |   1045 |
| FORD   | 3300 |  NULL |   3300 |
| MILLER | 1430 |  NULL |   1430 |
+--------+------+-------+--------+
13 rows in set (0.002 sec)
```
#### QUERY 8 :Display those employees who are working in sales or research?
```sql
 SELECT e.ename
    -> FROM employee e
    -> JOIN department d ON e.deptno = d.deptno
    -> WHERE d.dname IN ('SALES','RESEARCH');
+--------+
| ename  |
+--------+
| ALLEN  |
| WARD   |
| MARTIN |
| BLAKE  |
| TURNER |
| JAMES  |
| MILLER |
+--------+
7 rows in set (0.002 sec)
```
#### QUERY 9 : Display the grade of jones? 
```sql
 SELECT s.grade
    -> FROM employee e
    -> JOIN salgrade s ON e.sal BETWEEN s.lowsal AND s.highsal
    -> WHERE e.ename = 'JONES';
+-------+
| grade |
+-------+
|     5 |
+-------+
1 row in set (0.002 sec)
```
#### QUERY 10 : Display the department name the no of characters of which is equal to no of employees in any other department? 
```sql
SELECT d.dname
    -> FROM department d
    -> WHERE LENGTH(d.dname) IN (
    ->   SELECT COUNT(*) FROM employee e GROUP BY e.deptno );
Empty set (0.002 sec)
```
