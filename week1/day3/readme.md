# Day 3 - SQL Basics Practice
Below is the code for creating a table and insert the data into the table
CREATE TABLE Employees (
    emp_id INT,
    emp_name VARCHAR(50),
    department VARCHAR(50),
    salary INT,
    city VARCHAR(50),
    experience INT
);

INSERT INTO Employees VALUES
(101, 'Rahul', 'IT', 75000, 'Hyderabad', 5),
(102, 'Anjali', 'HR', 45000, 'Chennai', 3),
(103, 'Kiran', 'IT', 82000, 'Bangalore', 6),
(104, 'Sneha', 'Finance', 67000, 'Hyderabad', 4),
(105, 'Aman', 'HR', 39000, 'Pune', 2),
(106, 'Ravi', 'Finance', 91000, 'Mumbai', 8),
(107, 'Divya', 'IT', 55000, 'Chennai', 3),
(108, 'Meena', 'Sales', 48000, 'Bangalore', 2),
(109, 'Arjun', 'Sales', 61000, 'Hyderabad', 5),
(110, 'Pooja', 'IT', 73000, 'Mumbai', 4),
(111, 'Vikas', 'HR', 52000, 'Pune', 3),
(112, 'Nisha', 'Finance', 88000, 'Bangalore', 7),
(113, 'Tarun', 'Sales', 46000, 'Chennai', 2),
(114, 'Kavya', 'IT', 97000, 'Hyderabad', 9),
(115, 'Manoj', 'Finance', 58000, 'Mumbai', 4);
Edi data echaru naku 
Dani batti evi practice chyamanaru 
Below are the questions for practicing sql for you. Complete it
Questions
*SELECT*
Display all employee details.
Display only employee names and salaries.
Display employee names and departments.
Display all employees from the IT department.
Display employee names and experience.

*WHERE*
Find employees with salary greater than 70000.
Find employees working in Hyderabad.
Find employees with experience less than 4 years.
Find employees from Finance department.
Find employees whose salary is equal to 52000.

*GROUP BY*
Find total salary department-wise.
Find average salary in each department.
Count employees in each city.
Find maximum salary in each department.
Find minimum experience department-wise.

*HAVING*
Find departments having more than 3 employees.
Find departments where average salary is greater than 60000.
Find cities having more than 2 employees.
Find departments where total salary is greater than 200000.
Find departments where maximum salary is above 90000.

*TOP*
Display top 5 highest paid employees.
Display top 3 employees with highest experience.
Display top 2 salaries from Finance department.
Display top 4 employees from Hyderabad.
Display top 1 highest salary employee.

*DISTINCT*
Display distinct department names.
Display distinct city names.
Display distinct salary values.
Display distinct combinations of department and city.
Display distinct experience values.

*COMPARISON OPERATORS*
Find employees with salary >= 80000.
Find employees with experience <= 3.
Find employees whose salary <> 45000.
Find employees with salary < 50000.
Find employees with experience > 5.

*LOGICAL OPERATORS*
Find employees from IT department AND salary greater than 70000.
Find employees from Hyderabad OR Bangalore.
Find employees from HR department AND experience less than 3.
Find employees with salary greater than 60000 OR experience greater than 6.
Find employees NOT from Sales department.

*IN AND NOT IN*
Find employees working in ('Hyderabad', 'Mumbai').
Find employees whose department IN ('IT', 'Finance').
Find employees whose city NOT IN ('Chennai', 'Pune').
Find employees whose salary IN (45000, 75000, 91000).
Find employees whose department NOT IN ('HR', 'Sales').

*BETWEEN*
Find employees with salary BETWEEN 50000 AND 80000.
Find employees with experience BETWEEN 3 AND 6.
Find employees whose emp_id BETWEEN 105 AND 112.
Find employees with salary NOT BETWEEN 40000 AND 60000.
Find employees with experience BETWEEN 2 AND 4.

*LIKE OPERATOR*
Find employees whose names start with 'R'.
Find employees whose names end with 'a'.
Find employees whose names contain 'v'.
Find employees whose city starts with 'B'.
Find employees whose department ends with 's'. Nv explanation chyeee answer evvu
danilo half day1 laga evvu github lo post chyadaniki
ah queries  kuda evvu 
abba ala kadu nenu niku question echa kada avi kuda add chee anthunna mala github lo ma sir check chesinapudu denilo chesav antaru
## SELECT Queries

### 1. Display all employee details

```sql
SELECT * FROM Employees;
```

### 2. Display only employee names and salaries

```sql
SELECT emp_name, salary FROM Employees;
```

### 3. Display employee names and departments

```sql
SELECT emp_name, department FROM Employees;
```

### 4. Display all employees from the IT department

```sql
SELECT * FROM Employees
WHERE department = 'IT';
```

### 5. Display employee names and experience

```sql
SELECT emp_name, experience FROM Employees;
```

---

# WHERE Clause

### 1. Find employees with salary greater than 70000

```sql
SELECT * FROM Employees
WHERE salary > 70000;
```

### 2. Find employees working in Hyderabad

```sql
SELECT * FROM Employees
WHERE city = 'Hyderabad';
```

### 3. Find employees with experience less than 4 years

```sql
SELECT * FROM Employees
WHERE experience < 4;
```

### 4. Find employees from Finance department

```sql
SELECT * FROM Employees
WHERE department = 'Finance';
```

### 5. Find employees whose salary is equal to 52000

```sql
SELECT * FROM Employees
WHERE salary = 52000;
```

---

# DISTINCT

### 1. Display distinct department names

```sql
SELECT DISTINCT department
FROM Employees;
```

### 2. Display distinct city names

```sql
SELECT DISTINCT city
FROM Employees;
```

### 3. Display distinct salary values

```sql
SELECT DISTINCT salary
FROM Employees;
```

### 4. Display distinct combinations of department and city

```sql
SELECT DISTINCT department, city
FROM Employees;
```

### 5. Display distinct experience values

```sql
SELECT DISTINCT experience
FROM Employees;
```

