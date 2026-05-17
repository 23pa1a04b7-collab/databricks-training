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


## IN AND NOT IN

### Question 1: Find employees working in ('Hyderabad', 'Mumbai')

```sql
SELECT * FROM Employees
WHERE city IN ('Hyderabad', 'Mumbai');
```

### Question 2: Find employees whose department IN ('IT', 'Finance')

```sql
SELECT * FROM Employees
WHERE department IN ('IT', 'Finance');
```

### Question 3: Find employees whose city NOT IN ('Chennai', 'Pune')

```sql
SELECT * FROM Employees
WHERE city NOT IN ('Chennai', 'Pune');
```

### Question 4: Find employees whose salary IN (45000, 75000, 91000)

```sql
SELECT * FROM Employees
WHERE salary IN (45000, 75000, 91000);
```

### Question 5: Find employees whose department NOT IN ('HR', 'Sales')

```sql
SELECT * FROM Employees
WHERE department NOT IN ('HR', 'Sales');
```

---

# BETWEEN OPERATOR

### Question 1: Find employees with salary BETWEEN 50000 AND 80000

```sql
SELECT * FROM Employees
WHERE salary BETWEEN 50000 AND 80000;
```

### Question 2: Find employees with experience BETWEEN 3 AND 6

```sql
SELECT * FROM Employees
WHERE experience BETWEEN 3 AND 6;
```

### Question 3: Find employees whose emp_id BETWEEN 105 AND 112

```sql
SELECT * FROM Employees
WHERE emp_id BETWEEN 105 AND 112;
```

### Question 4: Find employees with salary NOT BETWEEN 40000 AND 60000

```sql
SELECT * FROM Employees
WHERE salary NOT BETWEEN 40000 AND 60000;
```

### Question 5: Find employees with experience BETWEEN 2 AND 4

```sql
SELECT * FROM Employees
WHERE experience BETWEEN 2 AND 4;
```

---

# LIKE OPERATOR

### Question 1: Find employees whose names start with 'R'

```sql
SELECT * FROM Employees
WHERE emp_name LIKE 'R%';
```

### Question 2: Find employees whose names end with 'a'

```sql
SELECT * FROM Employees
WHERE emp_name LIKE '%a';
```

### Question 3: Find employees whose names contain 'v'

```sql
SELECT * FROM Employees
WHERE emp_name LIKE '%v%';
```

### Question 4: Find employees whose city starts with 'B'

```sql
SELECT * FROM Employees
WHERE city LIKE 'B%';
```

### Question 5: Find employees whose department ends with 's'

```sql
SELECT * FROM Employees
WHERE department LIKE '%s';
```

