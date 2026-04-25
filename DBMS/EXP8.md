# EXPERIMENT 8
#### QUERY 1 : Display all employees with their dept name. 
 ```sql
SELECT e.ename, d.dname FROM employee e
 JOIN department d ON e.deptno = d.deptno;
 
+--------+------------+
| ename  | dname      |
+--------+------------+
| SMITH  | accounting |
| ALLEN  | sales      |
| WARD   | sales      |
| JONES  | accounting |
| MARTIN | sales      |
| BLAKE  | sales      |
| CLARK  | accounting |
| SCOTT  | operations |
| KING   | accounting |
| TURNER | sales      |
| ADAMS  | accounting |
| JAMES  | sales      |
| FORD   | accounting |
| MILLER | research   |
+--------+------------+
14 rows in set (0.002 sec)
```
#### QUERY 2 : Display those employees whose manager names is jones, and also display their manager name.
```sql
SELECT e.ename AS employee, m.ename AS manager FROM employee e
JOIN employee m ON e.mgr = m.empno WHERE m.ename = 'JONES';

+----------+---------+
| employee | manager |
+----------+---------+
| SCOTT    | JONES   |
| FORD     | JONES   |
+----------+---------+
2 rows in set (0.002 sec)
```
#### QUERY 3 : Display employee name, his job, his dept name, his manager name, his grade and make out of an under department wise.
```sql
SELECT e.ename, e.job, d.dname, m.ename AS manager, s.grade FROM employee e
   JOIN department d ON e.deptno = d.deptno
   JOIN salgrade s ON e.sal BETWEEN s.lowsal AND s.highsal
   LEFT JOIN employee m ON e.mgr = m.empno ORDER BY d.dname;
    
+--------+-----------+------------+---------+-------+
| ename  | job       | dname      | manager | grade |
+--------+-----------+------------+---------+-------+
| SMITH  | CLERK     | accounting | FORD    |     1 |
| ADAMS  | CLERK     | accounting | SCOTT   |     2 |
| CLARK  | MANAGER   | accounting | KING    |     4 |
| FORD   | ANALYST   | accounting | JONES   |     5 |
| JONES  | MANAGER   | accounting | KING    |     5 |
| KING   | PRESIDENT | accounting | NULL    |     5 |
| SCOTT  | ANALYST   | operations | JONES   |     5 |
| MILLER | CLERK     | research   | CLARK   |     3 |
| MARTIN | SALESMAN  | sales      | BLAKE   |     2 |
| TURNER | SALESMAN  | sales      | BLAKE   |     3 |
| BLAKE  | MANAGER   | sales      | KING    |     5 |
| ALLEN  | SALESMAN  | sales      | BLAKE   |     3 |
| JAMES  | CLERK     | sales      | BLAKE   |     1 |
| WARD   | SALESMAN  | sales      | BLAKE   |     2 |
+--------+-----------+------------+---------+-------+
14 rows in set (0.008 sec)
```
#### QUERY 4 : List out all the employees name, job, and salary grade and department name for everyone in the company except ‘clerk’. Sort on salary display the highest salary.
```sql
SELECT e.ename, e.job, e.sal, s.grade, d.dname FROM employee e
   JOIN department d ON e.deptno = d.deptno
   JOIN salgrade s ON e.sal BETWEEN s.lowsal AND s.highsal
   WHERE e.job <> 'CLERK' ORDER BY e.sal DESC;
   
+--------+-----------+------+-------+------------+
| ename  | job       | sal  | grade | dname      |
+--------+-----------+------+-------+------------+
| KING   | PRESIDENT | 5500 |     5 | accounting |
| FORD   | ANALYST   | 3300 |     5 | accounting |
| SCOTT  | ANALYST   | 3300 |     5 | operations |
| JONES  | MANAGER   | 3273 |     5 | accounting |
| BLAKE  | MANAGER   | 3135 |     5 | sales      |
| CLARK  | MANAGER   | 2695 |     4 | accounting |
| TURNER | SALESMAN  | 1650 |     3 | sales      |
| ALLEN  | SALESMAN  | 1600 |     3 | sales      |
| MARTIN | SALESMAN  | 1250 |     2 | sales      |
| WARD   | SALESMAN  | 1250 |     2 | sales      |
+--------+-----------+------+-------+------------+
10 rows in set (0.001 sec)
```
#### QUERY 5 : Display employee name, his job and his manager. Display also employees who are without manager. 
```sql
SELECT e.ename, e.job, COALESCE(m.ename, 'NO MANAGER') AS manager FROM employee e
   LEFT JOIN employee m ON e.mgr = m.empno;
   
+--------+-----------+------------+
| ename  | job       | manager    |
+--------+-----------+------------+
| SMITH  | CLERK     | FORD       |
| ALLEN  | SALESMAN  | BLAKE      |
| WARD   | SALESMAN  | BLAKE      |
| JONES  | MANAGER   | KING       |
| MARTIN | SALESMAN  | BLAKE      |
| BLAKE  | MANAGER   | KING       |
| CLARK  | MANAGER   | KING       |
| SCOTT  | ANALYST   | JONES      |
| KING   | PRESIDENT | NO MANAGER |
| TURNER | SALESMAN  | BLAKE      |
| ADAMS  | CLERK     | SCOTT      |
| JAMES  | CLERK     | BLAKE      |
| FORD   | ANALYST   | JONES      |
| MILLER | CLERK     | CLARK      |
+--------+-----------+------------+
14 rows in set (0.001 sec)
```
#### QUERY 6 : List the employee name, job, annual salary, deptno, dept name and grade who earn 36000 a year or who are not clerks. 
```sql
SELECT e.ename, e.job, (e.sal*12) AS annual_sal, e.deptno, d.dname, s.grade FROM employee e
 JOIN department d ON e.deptno = d.deptno
 JOIN salgrade s ON e.sal BETWEEN s.lowsal AND s.highsal
 WHERE (e.sal*12 = 36000) OR (e.job <> 'CLERK');
    
+--------+-----------+------------+--------+------------+-------+
| ename  | job       | annual_sal | deptno | dname      | grade |
+--------+-----------+------------+--------+------------+-------+
| ALLEN  | SALESMAN  |      19200 |     30 | sales      |     3 |
| WARD   | SALESMAN  |      15000 |     30 | sales      |     2 |
| JONES  | MANAGER   |      39276 |     20 | accounting |     5 |
| MARTIN | SALESMAN  |      15000 |     30 | sales      |     2 |
| BLAKE  | MANAGER   |      37620 |     30 | sales      |     5 |
| CLARK  | MANAGER   |      32340 |     20 | accounting |     4 |
| SCOTT  | ANALYST   |      39600 |     40 | operations |     5 |
| KING   | PRESIDENT |      66000 |     20 | accounting |     5 |
| TURNER | SALESMAN  |      19800 |     30 | sales      |     3 |
| FORD   | ANALYST   |      39600 |     20 | accounting |     5 |
+--------+-----------+------------+--------+------------+-------+
10 rows in set (0.002 sec)
```
#### QUERY 7 : List ename, job, annual sal, deptno, dname and grade who earn 30000 per year and who are not clerks. 
 ```sql
SELECT e.ename, e.job, (e.sal*12) AS annual_sal, e.deptno, d.dname, s.grade FROM employee e
 JOIN department d ON e.deptno = d.deptno
 JOIN salgrade s ON e.sal BETWEEN s.lowsal AND s.highsal
 WHERE (e.sal*12 = 30000) AND (e.job <> 'CLERK');
 
Empty set (0.001 sec)
```
#### QUERY 8 : List out all employees by name and number along with their manager’s name and number also display ‘no manager’ who has no manager. 
```sql
SELECT e.empno, e.ename,
COALESCE(m.empno, 'NO MANAGER') AS mgr_no,
COALESCE(m.ename, 'NO MANAGER') AS mgr_name FROM employee e
LEFT JOIN employee m ON e.mgr = m.empno;

+-------+--------+------------+------------+
| empno | ename  | mgr_no     | mgr_name   |
+-------+--------+------------+------------+
|  7369 | SMITH  | 7902       | FORD       |
|  7499 | ALLEN  | 7698       | BLAKE      |
|  7521 | WARD   | 7698       | BLAKE      |
|  7566 | JONES  | 7839       | KING       |
|  7654 | MARTIN | 7698       | BLAKE      |
|  7698 | BLAKE  | 7839       | KING       |
|  7782 | CLARK  | 7839       | KING       |
|  7788 | SCOTT  | 7566       | JONES      |
|  7839 | KING   | NO MANAGER | NO MANAGER |
|  7844 | TURNER | 7698       | BLAKE      |
|  7876 | ADAMS  | 7788       | SCOTT      |
|  7900 | JAMES  | 7698       | BLAKE      |
|  7902 | FORD   | 7566       | JONES      |
|  7934 | MILLER | 7782       | CLARK      |
+-------+--------+------------+------------+
14 rows in set (0.001 sec)
```
#### QUERY 9 : Select dept name, dept no and sum of sal.
```sql
SELECT d.dname, d.deptno, SUM(e.sal) AS total_sal FROM employee e
 JOIN department d ON e.deptno = d.deptno
 GROUP BY d.dname, d.deptno;
 
+------------+--------+-----------+
| dname      | deptno | total_sal |
+------------+--------+-----------+
| accounting |     20 |     16858 |
| operations |     40 |      3300 |
| research   |     10 |      1430 |
| sales      |     30 |      9930 |
+------------+--------+-----------+
4 rows in set (0.002 sec)
```
#### QUERY 10 : Display employee number, name and location of the department in which he is working.
```sql
SELECT e.empno, e.ename, d.location FROM employee e
JOIN department d ON e.deptno = d.deptno;

+-------+--------+------------+
| empno | ename  | location   |
+-------+--------+------------+
|  7369 | SMITH  | FRANCE     |
|  7499 | ALLEN  | LOS ANGLES |
|  7521 | WARD   | LOS ANGLES |
|  7566 | JONES  | FRANCE     |
|  7654 | MARTIN | LOS ANGLES |
|  7698 | BLAKE  | LOS ANGLES |
|  7782 | CLARK  | FRANCE     |
|  7788 | SCOTT  | INDIA      |
|  7839 | KING   | FRANCE     |
|  7844 | TURNER | LOS ANGLES |
|  7876 | ADAMS  | FRANCE     |
|  7900 | JAMES  | LOS ANGLES |
|  7902 | FORD   | FRANCE     |
|  7934 | MILLER | NEW YORK   |
+-------+--------+------------+
14 rows in set (0.001 sec)
```
#### QUERY 11 : Display employee name and department name for each employee.
 ```sql
SELECT e.ename, d.dname FROM employee e
 JOIN department d ON e.deptno = d.deptno;
 
+--------+------------+
| ename  | dname      |
+--------+------------+
| SMITH  | accounting |
| ALLEN  | sales      |
| WARD   | sales      |
| JONES  | accounting |
| MARTIN | sales      |
| BLAKE  | sales      |
| CLARK  | accounting |
| SCOTT  | operations |
| KING   | accounting |
| TURNER | sales      |
| ADAMS  | accounting |
| JAMES  | sales      |
| FORD   | accounting |
| MILLER | research   |
+--------+------------+
14 rows in set (0.001 sec)
```
