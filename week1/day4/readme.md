# Day 4 - SQL Basics Practice

## COMPARISON OPERATORS

### Question 1: Find employees with salary >= 80000

```sql
SELECT * FROM Employees
WHERE salary >= 80000;
```

### Question 2: Find employees with experience <= 3

```sql
SELECT * FROM Employees
WHERE experience <= 3;
```

### Question 3: Find employees whose salary <> 45000

```sql
SELECT * FROM Employees
WHERE salary <> 45000;
```

### Question 4: Find employees with salary < 50000

```sql
SELECT * FROM Employees
WHERE salary < 50000;
```

### Question 5: Find employees with experience > 5

```sql
SELECT * FROM Employees
WHERE experience > 5;
```

---

# LOGICAL OPERATORS

### Question 1: Find employees from IT department AND salary greater than 70000

```sql
SELECT * FROM Employees
WHERE department = 'IT'
AND salary > 70000;
```

### Question 2: Find employees from Hyderabad OR Bangalore

```sql
SELECT * FROM Employees
WHERE city = 'Hyderabad'
OR city = 'Bangalore';
```

### Question 3: Find employees from HR department AND experience less than 3

```sql
SELECT * FROM Employees
WHERE department = 'HR'
AND experience < 3;
```

### Question 4: Find employees with salary greater than 60000 OR experience greater than 6

```sql
SELECT * FROM Employees
WHERE salary > 60000
OR experience > 6;
```

### Question 5: Find employees NOT from Sales department

```sql
SELECT * FROM Employees
WHERE department != 'Sales';
```

