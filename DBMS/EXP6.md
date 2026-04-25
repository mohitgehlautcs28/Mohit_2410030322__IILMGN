# EXPERIMENT 6
#### QUERY 1: Display empno, ename, deptno from employee table. Instead of display department numbers display the related department name . 
```sql
SELECT EMPNO,ENAME,CASE deptno
    -> WHEN 10 THEN 'RESEARCH'
    -> WHEN 20 THEN 'ACCOUNTING'
    -> WHEN 30 THEN 'SALES'
    -> WHEN 40 THEN 'OPERATIONS'
    -> END AS DNAME FROM EMPLOYEE;
+-------+--------+------------+
| EMPNO | ENAME  | DNAME      |
+-------+--------+------------+
|  7369 | SMITH  | ACCOUNTING |
|  7499 | ALLEN  | SALES      |
|  7521 | WARD   | SALES      |
|  7566 | JONES  | ACCOUNTING |
|  7654 | MARTIN | SALES      |
|  7698 | BLAKE  | SALES      |
|  7782 | CLARK  | ACCOUNTING |
|  7788 | SCOTT  | OPERATIONS |
|  7839 | KING   | ACCOUNTING |
|  7844 | TURNER | SALES      |
|  7876 | ADAMS  | ACCOUNTING |
|  7900 | JAMES  | SALES      |
|  7902 | FORD   | ACCOUNTING |
|  7934 | MILLER | RESEARCH   |
+-------+--------+------------+
14 rows in set (0.028 sec)

```
#### QUERY 2: Display your age in days
```sql
SELECT DATEDIFF('2026-02-17','2006-03-29') AS AGE_IN_DAYS;
+-------------+
| AGE_IN_DAYS |
+-------------+
|        7265 |
+-------------+
1 row in set (0.001 sec)

```
#### QUERY 3: Display your age in months. 
```sql
SELECT TIMESTAMPDIFF(MONTH,'2006-03-29',CURDATE()) AS AGE_IN_MONTHS;
+---------------+
| AGE_IN_MONTHS |
+---------------+
|           238 |
+---------------+
1 row in set (0.001 sec)

```
#### QUERY 4: Display the current date as 15th August Friday Nineteen Ninety-Seven. 
```sql
SELECT DATE_FORMAT('1997-08-15','%D %M %W %Y');
+-----------------------------------------+
| DATE_FORMAT('1997-08-15','%D %M %W %Y') |
+-----------------------------------------+
| 15th August Friday 1997                 |
+-----------------------------------------+
1 row in set (0.001 sec)

```
#### QUERY 5: Find the date for nearest Saturday after current date.
```sql
SELECT DATE_ADD(CURDATE(),INTERVAL(7-DAYOFWEEK(CURDATE()))DAY) AS NEAREST_SATURDAY;
+------------------+
| NEAREST_SATURDAY |
+------------------+
| 2026-02-21       |
+------------------+
1 row in set (0.001 sec)

```
#### QUERY 6: Display current time. 
```sql
SELECT CURTIME();
+-----------+
| CURTIME() |
+-----------+
| 16:40:06  |
+-----------+
1 row in set (0.001 sec)
```
#### QUERY 7: Display the date three months Before the current date 
```sql
SELECT DATE_SUB(CURDATE(),INTERVAL 3 MONTH);
+--------------------------------------+
| DATE_SUB(CURDATE(),INTERVAL 3 MONTH) |
+--------------------------------------+
| 2025-11-17                           |
+--------------------------------------+
1 row in set (0.001 sec)

```
#### QUERY 8: Display those employees who joined in the company in the month of Dec. 
```sql
SELECT * FROM EMPLOYEE WHERE MONTH(HIREDATE) =12;
+-------+-------+---------+------+------------+------+-------+--------+
| empno | ename | job     | mgr  | hiredate   | sal  | compp | deptno |
+-------+-------+---------+------+------------+------+-------+--------+
|  7369 | SMITH | CLERK   | 7902 | 1980-12-17 |  880 |  NULL |     20 |
|  7788 | SCOTT | ANALYST | 7566 | 1982-12-09 | 3300 |  NULL |     40 |
|  7900 | JAMES | CLERK   | 7698 | 1981-12-03 | 1045 |  NULL |     30 |
|  7902 | FORD  | ANALYST | 7566 | 1981-12-03 | 3300 |  NULL |     20 |
+-------+-------+---------+------+------------+------+-------+--------+
4 rows in set (0.002 sec)
```
#### QUERY 9:  Display those employees who joined the company before 15 of the months.
```sql
SELECT * FROM EMPLOYEE WHERE DAY(HIREDATE) <=15;
+-------+--------+----------+------+------------+------+-------+--------+
| empno | ename  | job      | mgr  | hiredate   | sal  | compp | deptno |
+-------+--------+----------+------+------------+------+-------+--------+
|  7566 | JONES  | MANAGER  | 7839 | 1981-04-02 | 3273 |  NULL |     20 |
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 3135 |  NULL |     30 |
|  7782 | CLARK  | MANAGER  | 7839 | 1981-06-09 | 2695 |  NULL |     20 |
|  7788 | SCOTT  | ANALYST  | 7566 | 1982-12-09 | 3300 |  NULL |     40 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1650 |     0 |     30 |
|  7876 | ADAMS  | CLERK    | 7788 | 1983-01-12 | 1210 |  NULL |     20 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 | 1045 |  NULL |     30 |
|  7902 | FORD   | ANALYST  | 7566 | 1981-12-03 | 3300 |  NULL |     20 |
+-------+--------+----------+------+------------+------+-------+--------+
8 rows in set (0.001 sec)
```
#### QUERY 10: Display those employees whose joining DATE is available in deptno 
```sql
SELECT ENAME, HIREDATE, DEPTNO
     FROM EMPLOYEE
     WHERE DAY(HIREDATE) = DEPTNO;
Empty set (0.001 sec)

```
