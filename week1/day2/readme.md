# Day 2 SQL Practice

## Order By Queries

### 31. Employees ordered by salary ascending

```sql
SELECT * FROM Employee
ORDER BY salary ASC;
```

### 32. Employees ordered by age descending

```sql
SELECT * FROM Employee
ORDER BY age DESC;
```

### 33. Employees ordered by hire date ascending

```sql
SELECT * FROM Employee
ORDER BY hire_date ASC;
```

### 34. Employees ordered by department then salary

```sql
SELECT * FROM Employee
ORDER BY department_id, salary;
```

### 35. Departments ordered by total salary

```sql
SELECT department_id, SUM(salary) AS total_salary
FROM Employee
GROUP BY department_id
ORDER BY total_salary DESC;
```

## Join Queries

### 36. Employee names with department names

```sql
SELECT e.name AS employee_name,
d.name AS department_name
FROM Employee e
JOIN Department d
ON e.department_id = d.department_id;
```

### 37. Project names with department names

```sql
SELECT p.name AS project_name,
d.name AS department_name
FROM Project p
JOIN Department d
ON p.department_id = d.department_id;
```

### 38. Employee names with project names

```sql
SELECT e.name AS employee_name,
p.name AS project_name
FROM Employee e
JOIN Project p
ON e.department_id = p.department_id;
```

### 39. All employees with departments

```sql
SELECT e.name, d.name
FROM Employee e
LEFT JOIN Department d
ON e.department_id = d.department_id;
```

### 40. All departments with employees

```sql
SELECT d.name, e.name
FROM Department d
LEFT JOIN Employee e
ON d.department_id = e.department_id;
```

### 41. Employees not assigned any project

```sql
SELECT e.name
FROM Employee e
LEFT JOIN Project p
ON e.department_id = p.department_id
WHERE p.project_id IS NULL;
```

### 42. Employees and number of projects

```sql
SELECT e.name,
COUNT(p.project_id) AS total_projects
FROM Employee e
LEFT JOIN Project p
ON e.department_id = p.department_id
GROUP BY e.emp_id, e.name;
```

### 43. Departments with no employees

```sql
SELECT d.name
FROM Department d
LEFT JOIN Employee e
ON d.department_id = e.department_id
WHERE e.emp_id IS NULL;
```

### 44. Employees in same department as John Doe

```sql
SELECT name
FROM Employee
WHERE department_id = (
SELECT department_id
FROM Employee
WHERE name = 'John Doe'
);
```

### 45. Department with highest average salary

```sql
SELECT d.name, AVG(e.salary) AS avg_salary
FROM Employee e
JOIN Department d
ON e.department_id = d.department_id
GROUP BY d.name
ORDER BY avg_salary DESC
LIMIT 1;
```

## Nested and Correlated Queries

### 46. Employee with highest salary

```sql
SELECT *
FROM Employee
WHERE salary = (
SELECT MAX(salary)
FROM Employee
);
```

### 47. Employees salary above average

```sql
SELECT *
FROM Employee
WHERE salary > (
SELECT AVG(salary)
FROM Employee
);
```

### 48. Second highest salary

```sql
SELECT MAX(salary)
FROM Employee
WHERE salary < (
SELECT MAX(salary)
FROM Employee
);
```

### 49. Department with most employees

```sql
SELECT department_id,
COUNT(*) AS total
FROM Employee
GROUP BY department_id
ORDER BY total DESC
LIMIT 1;
```

### 50. Employees earning more than department average

```sql
SELECT *
FROM Employee e
WHERE salary > (
SELECT AVG(salary)
FROM Employee
WHERE department_id = e.department_id
);
```

### 51. Third highest salary

```sql
SELECT DISTINCT salary
FROM Employee
ORDER BY salary DESC
LIMIT 1 OFFSET 2;
```

### 52. Employees older than all HR employees

```sql
SELECT *
FROM Employee
WHERE age > ALL (
SELECT age
FROM Employee e
JOIN Department d
ON e.department_id = d.department_id
WHERE d.name = 'HR'
);
```

### 53. Departments with avg salary > 55000

```sql
SELECT department_id
FROM Employee
GROUP BY department_id
HAVING AVG(salary) > 55000;
```

### 54. Employees in departments with at least 2 projects

```sql
SELECT *
FROM Employee
WHERE department_id IN (
SELECT department_id
FROM Project
GROUP BY department_id
HAVING COUNT(*) >= 2
);
```

### 55. Employees hired same date as Jane Smith

```sql
SELECT *
FROM Employee
WHERE hire_date = (
SELECT hire_date
FROM Employee
WHERE name = 'Jane Smith'
);
```

## Combined Moderate Difficulty Queries

### 56. Total salary of employees hired in 2020

```sql
SELECT SUM(salary) AS total_salary
FROM Employee
WHERE YEAR(hire_date) = 2020;
```

### 57. Avg salary by department descending

```sql
SELECT department_id,
AVG(salary) AS avg_salary
FROM Employee
GROUP BY department_id
ORDER BY avg_salary DESC;
```

### 58. Departments with >1 employee and avg salary >55000

```sql
SELECT department_id
FROM Employee
GROUP BY department_id
HAVING COUNT(*) > 1
AND AVG(salary) > 55000;
```

### 59. Employees hired in last 2 years ordered by hire date

```sql
SELECT *
FROM Employee
WHERE hire_date >= CURDATE() - INTERVAL 2 YEAR
ORDER BY hire_date;
```

### 60. Total employees and avg salary for departments with >2 employees

```sql
SELECT department_id,
COUNT(*) AS total_employees,
AVG(salary) AS avg_salary
FROM Employee
GROUP BY department_id
HAVING COUNT(*) > 2;
```

### 61. Employees whose salary above department average

```sql
SELECT name, salary
FROM Employee e
WHERE salary > (
SELECT AVG(salary)
FROM Employee
WHERE department_id = e.department_id
);
```

### 62. Employees hired same date as oldest employee

```sql
SELECT name
FROM Employee
WHERE hire_date = (
SELECT hire_date
FROM Employee
ORDER BY age DESC
LIMIT 1
);
```

### 63. Department names with total projects

```sql
SELECT d.name,
COUNT(p.project_id) AS total_projects
FROM Department d
LEFT JOIN Project p
ON d.department_id = p.department_id
GROUP BY d.name
ORDER BY total_projects DESC;
```

### 64. Highest salary employee in each department

```sql
SELECT e.name, e.salary, e.department_id
FROM Employee e
WHERE salary = (
SELECT MAX(salary)
FROM Employee
WHERE department_id = e.department_id
);
```

### 65. Employees older than avg age of department

```sql
SELECT name, salary
FROM Employee e
WHERE age > (
SELECT AVG(age)
FROM Employee
WHERE department_id = e.department_id
);
```
