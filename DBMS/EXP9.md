# EXPERIMENT 9
#### QUERY 1 : Display the name of emp name who earns highest salary. 
```sql
SELECT enameFROM employee WHERE sal = (SELECT MAX(sal) FROM employee);

+-------+
| ename |
+-------+
| KING  |
+-------+
1 row in set (0.075 sec)
```
#### QUERY 2 : Display the employee number and name of employee working as clerk and earning highest salary among clerks. 
```sql
SELECT empno, enameFROM employee WHERE job = 'CLERK'
 AND sal = (SELECT MAX(sal) FROM employee WHERE job = 'CLERK');
 
+-------+--------+
| empno | ename  |
+-------+--------+
|  7934 | MILLER |
+-------+--------+
1 row in set (0.004 sec)
```
#### QUERY 3 : Display the names of the salesman who earns a salary more than the highest salary of any clerk.
```sql
SELECT ename FROM employee WHERE job = 'SALESMAN'
AND sal > (SELECT MAX(sal) FROM employee WHERE job = 'CLERK');

+--------+
| ename  |
+--------+
| ALLEN  |
| TURNER |
+--------+
2 rows in set (0.001 sec)
```
#### QUERY 4 :Display the names of clerks who earn salary more than that of james of that of sal lesser than that of scott.
 ```sql
SELECT ename FROM employee WHERE job = 'CLERK'
 AND sal > (SELECT sal FROM employee WHERE ename = 'JAMES')
 AND sal < (SELECT sal FROM employee WHERE ename = 'SCOTT');
 
+--------+
| ename  |
+--------+
| ADAMS  |
| MILLER |
+--------+
2 rows in set (0.002 sec)
```
#### QUERY 5 : Display the names of employees who earn a sal more than that of james or that of salary greater than that of scott.
 ```sql
SELECT ename FROM employee
 WHERE sal > (SELECT sal FROM employee WHERE ename = 'JAMES')
 OR sal > (SELECT sal FROM employee WHERE ename = 'SCOTT');
 
+--------+
| ename  |
+--------+
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| BLAKE  |
| CLARK  |
| SCOTT  |
| KING   |
| TURNER |
| ADAMS  |
| FORD   |
| MILLER |
+--------+
12 rows in set (0.001 sec)
```
#### QUERY 6 : Display the names of the employees who earn highest salary in their respective departments. 
```sql
SELECT ename, deptno FROM employee e
 WHERE sal = (SELECT MAX(sal)  FROM employee WHERE deptno = e.deptno);
 
+--------+--------+
| ename  | deptno |
+--------+--------+
| BLAKE  |     30 |
| SCOTT  |     40 |
| KING   |     20 |
| MILLER |     10 |
+--------+--------+
4 rows in set (0.001 sec)
```
#### QUERY 7 : Display the names of employees who earn highest salaries in their respective job groups. 
```sql
SELECT ename, job FROM employee e
 WHERE sal = ( SELECT MAX(sal) FROM employee WHERE job = e.job);
 
+--------+-----------+
| ename  | job       |
+--------+-----------+
| JONES  | MANAGER   |
| SCOTT  | ANALYST   |
| KING   | PRESIDENT |
| TURNER | SALESMAN  |
| FORD   | ANALYST   |
| MILLER | CLERK     |
+--------+-----------+
6 rows in set (0.001 sec)
```
#### QUERY 8 : Display the employee names who are working in accounting dept. 
```sql
SELECT ename FROM employee
 WHERE deptno = (SELECT deptno FROM department WHERE dname = 'ACCOUNTING');
 
+-------+
| ename |
+-------+
| SMITH |
| JONES |
| CLARK |
| KING  |
| ADAMS |
| FORD  |
+-------+
6 rows in set (0.007 sec)
```
#### QUERY 9 : Display the employee names who are working in France.
```sql
SELECT ename FROM employee
WHERE deptno = (SELECT deptno FROM department WHERE location = 'FRANCE');

+-------+
| ename |
+-------+
| SMITH |
| JONES |
| CLARK |
| KING  |
| ADAMS |
| FORD  |
+-------+
6 rows in set (0.001 sec)
```
#### QUERY 10 :  Display the job groups having total salary greater than the maximum salary for managers.
 ```sql
SELECT job FROM employee GROUP BY job
 HAVING SUM(sal) > (SELECT MAX(sal) FROM employee WHERE job = 'MANAGER');
 
+-----------+
| job       |
+-----------+
| ANALYST   |
| CLERK     |
| MANAGER   |
| PRESIDENT |
| SALESMAN  |
+-----------+
5 rows in set (0.002 sec)
```
