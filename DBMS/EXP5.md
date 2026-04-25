# EXPERIMENT 5
#### QUERY 1: Display the total number of employee working in the company. 
```sql
SELECT COUNT(*) AS TOTAL_EMP FROM EMPLOYEE;
+--------------+
|     TOTAL_EMP|
+--------------+
|           14 |
+--------------+
1 row in set (0.001 sec)

```
#### QUERY 2: Display the total salary being paid to all employees. 
```sql
SELECT SUM(SAL) AS TOTAL_SALARY FROM EMPLOYEE;
+--------------+
| TOTAL_SALARY |
+--------------+
|        29025 |
+--------------+
1 row in set (0.075 sec)
```
#### QUERY 3: Display the maximum salary from employee table.
```sql
SELECT MAX(SAL) AS MAX_SALARY FROM EMPLOYEE;
+--------------+
|   MAX_SALARY |
+--------------+
|         5000 |
+--------------+
1 row in set (0.002 sec)

```
#### QUERY 4: Display the minimum salary from employee table. 
```sql
SELECT MIN(SAL) AS MIN_SALARY FROM EMPLOYEE;
+--------------+
|   MIN_SALARY |
+--------------+
|          800 |
+--------------+
1 row in set (0.001 sec)

```
#### QUERY 5: Display the average salary from employee table 
```sql
SELECT AVG(SAL) AS AVG_SALARY FROM EMPLOYEE;
+--------------+
|   AVG_SALARY |
+--------------+
|    2073.2143 |
+--------------+
1 row in set (0.001 sec)
```
#### QUERY 6: Display the maximum salary being paid to clerk. 
```sql
SELECT MAX(SAL) AS MAX_SALARY FROM EMPLOYEE WHERE JOB = 'CLERK' ;
+--------------+
|   MAX_SALARY |
+--------------+
|         1300 |
+--------------+
1 row in set (0.001 sec)
```
#### QUERY 7: Display the maximum salary being paid in dept no 20. 
```sql
SELECT MAX(SAL) AS MAX_SALARY FROM EMPLOYEE WHERE DEPTNO = 20 ;
+--------------+
|   MAX_SALARY |
+--------------+
|         5000 |
+--------------+
1 row in set (0.001 sec)

```
#### QUERY 8: Display the minimum salary paid to any salesman.
```sql
SELECT MIN(SAL) AS MIN_SALARY FROM EMPLOYEE WHERE JOB = 'SALESMAN' ;
+--------------+
|   MIN_SALARY |
+--------------+
|         1250 |
+--------------+
1 row in set (0.001 sec)
```
#### QUERY 9: Display the average salary drawn by managers. 
```sql
SELECT AVG(SAL) AS AVG_SAL FROM EMPLOYEE WHERE JOB = 'MANAGER';
+-----------+
| AVG_SAL   |
+-----------+
| 3024.3333 |
+-----------+
1 row in set (0.001 sec)

```
#### QUERY 10: Display the total salary drawn by analyst working in dept no 40. 
```sql
SELECT SUM(SAL) AS TOTAL_SAL FROM EMPLOYEE WHERE JOB = 'ANALYST' AND DEPTNO = 40;
+-----------+
| TOTAL_SAL |
+-----------+
|      3300 |
+-----------+
1 row in set (0.004 sec)
```
#### QUERY 11: Display the names of the employee in Uppercase
```sql
SELECT UPPER(ENAME) AS TOTAL_SAL FROM EMPLOYEE;
+-----------+
| TOTAL_SAL |
+-----------+
| SMITH     |
| ALLEN     |
| WARD      |
| JONES     |
| MARTIN    |
| BLAKE     |
| CLARK     |
| SCOTT     |
| KING      |
| TURNER    |
| ADAMS     |
| JAMES     |
| FORD      |
| MILLER    |
+-----------+
14 rows in set (0.001 sec)
```
#### QUERY 12: Display the names of the employee in Lowercase. 
```sql
SELECT LOWER(ENAME) AS TOTAL_SAL FROM EMPLOYEE;
+-----------+
| TOTAL_SAL |
+-----------+
| smith     |
| allen     |
| ward      |
| jones     |
| martin    |
| blake     |
| clark     |
| scott     |
| king      |
| turner    |
| adams     |
| james     |
| ford      |
| miller    |
+-----------+
14 rows in set (0.002 sec)
```
#### QUERY 13: Display the names of the employee in Proper case. 
```sql
SELECT CONCAT(
    ->        UPPER(SUBSTRING(ename,1,1)),
    ->        LOWER(SUBSTRING(ename,2))
    ->        ) AS Proper_name
    -> FROM EMPLOYEE;
+-------------+
| Proper_name |
+-------------+
| Smith       |
| Allen       |
| Ward        |
| Jones       |
| Martin      |
| Blake       |
| Clark       |
| Scott       |
| King        |
| Turner      |
| Adams       |
| James       |
| Ford        |
| Miller      |
+-------------+
14 rows in set (0.002 sec)

```
#### QUERY 14: Display the length of Your name using appropriate function. 
```sql
SELECT LENGTH('Abhijit Chaudhary') AS Name_Length;
+-------------+
| Name_Length |
+-------------+
|          17 |
+-------------+
1 row in set (0.002 sec)
```
#### QUERY 15: Display the length of all the employee names.
```sql
SELECT LENGTH(Ename) AS Name_Length FROM EMPLOYEE;
+-------------+
| Name_Length |
+-------------+
|           5 |
|           5 |
|           4 |
|           5 |
|           6 |
|           5 |
|           5 |
|           5 |
|           4 |
|           6 |
|           5 |
|           5 |
|           4 |
|           6 |
+-------------+
14 rows in set (0.002 sec)
```
