# Day 1 SQL Practice

## Basic Queries

### 1. Select all columns from the Employee table

```sql
SELECT * FROM Employee;
```

### 2. Select only the name and salary columns

```sql
SELECT name, salary FROM Employee;
```

### 3. Select employees who are older than 30

```sql
SELECT * FROM Employee
WHERE age > 30;
```

### 4. Select the names of all departments

```sql
SELECT name FROM Department;
```

### 5. Select employees who work in the IT department

```sql
SELECT e.*
FROM Employee e
JOIN Department d
ON e.department_id = d.department_id
WHERE d.name = 'IT';
```

## String Matching Queries

### 6. Names start with J

```sql
SELECT * FROM Employee
WHERE name LIKE 'J%';
```

### 7. Names end with e

```sql
SELECT * FROM Employee
WHERE name LIKE '%e';
```

### 8. Names contain a

```sql
SELECT * FROM Employee
WHERE name LIKE '%a%';
```

### 9. Names exactly 9 characters

```sql
SELECT * FROM Employee
WHERE LENGTH(name) = 9;
```

### 10. Second character is o

```sql
SELECT * FROM Employee
WHERE name LIKE '_o%';
```

## Date Queries

### 11. Employees hired in 2020

```sql
SELECT * FROM Employee
WHERE YEAR(hire_date) = 2020;
```

### 12. Employees hired in January

```sql
SELECT * FROM Employee
WHERE MONTH(hire_date) = 1;
```

### 13. Employees hired before 2019

```sql
SELECT * FROM Employee
WHERE hire_date < '2019-01-01';
```

### 14. Employees hired on or after March 1, 2021

```sql
SELECT * FROM Employee
WHERE hire_date >= '2021-03-01';
```

### 15. Employees hired in last 2 years

```sql
SELECT * FROM Employee
WHERE hire_date >= CURDATE() - INTERVAL 2 YEAR;
```

## Aggregate Queries

### 16. Total salary

```sql
SELECT SUM(salary) AS total_salary
FROM Employee;
```

### 17. Average salary

```sql
SELECT AVG(salary) AS avg_salary
FROM Employee;
```

### 18. Minimum salary

```sql
SELECT MIN(salary) AS min_salary
FROM Employee;
```

### 19. Number of employees in each department

```sql
SELECT department_id, COUNT(*) AS total_employees
FROM Employee
GROUP BY department_id;
```

### 20. Average salary in each department

```sql
SELECT department_id, AVG(salary) AS avg_salary
FROM Employee
GROUP BY department_id;
```

### 21. Total salary for each department

```sql
SELECT department_id, SUM(salary) AS total_salary
FROM Employee
GROUP BY department_id;
```

### 22. Average age in each department

```sql
SELECT department_id, AVG(age) AS avg_age
FROM Employee
GROUP BY department_id;
```

### 23. Number of employees hired each year

```sql
SELECT YEAR(hire_date) AS hire_year,
COUNT(*) AS total
FROM Employee
GROUP BY YEAR(hire_date);
```

### 24. Highest salary in each department

```sql
SELECT department_id, MAX(salary) AS highest_salary
FROM Employee
GROUP BY department_id;
```

### 25. Department with highest average salary

```sql
SELECT department_id, AVG(salary) AS avg_salary
FROM Employee
GROUP BY department_id
ORDER BY avg_salary DESC
LIMIT 1;
```

### 26. Departments with more than 2 employees

```sql
SELECT department_id, COUNT(*) AS total
FROM Employee
GROUP BY department_id
HAVING COUNT(*) > 2;
```

### 27. Departments with avg salary > 55000

```sql
SELECT department_id, AVG(salary) AS avg_salary
FROM Employee
GROUP BY department_id
HAVING AVG(salary) > 55000;
```

### 28. Years with more than 1 employee hired

```sql
SELECT YEAR(hire_date) AS hire_year,
COUNT(*) AS total
FROM Employee
GROUP BY YEAR(hire_date)
HAVING COUNT(*) > 1;
```

### 29. Departments with total salary less than 100000

```sql
SELECT department_id, SUM(salary) AS total_salary
FROM Employee
GROUP BY department_id
HAVING SUM(salary) < 100000;
```

### 30. Departments with max salary above 75000

```sql
SELECT department_id, MAX(salary) AS max_salary
FROM Employee
GROUP BY department_id
HAVING MAX(salary) > 75000;
```
