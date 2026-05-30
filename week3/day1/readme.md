         Joins.docxs
# SQL JOINS ASSIGNMENT

## Question 1
Retrieve the names of employees and their corresponding managers from the employees table, ensuring that even employees without managers are included.

```sql
SELECT e.emp_name AS Employee,
       m.emp_name AS Manager
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.emp_id;
```

## Question 2
Display all employees and their corresponding departments from the employees and departments tables, showing employees even if they don't belong to any department.

```sql
SELECT e.emp_name,
       d.dept_name
FROM employees e
LEFT JOIN departments d
ON e.dept_id = d.dept_id;
```

## Question 3
List the names of employees who report to a manager, along with their manager's name.

```sql
SELECT e.emp_name AS Employee,
       m.emp_name AS Manager
FROM employees e
INNER JOIN employees m
ON e.manager_id = m.emp_id;
```

## Question 4
Find the total salary paid to each employee and their respective department, including departments with no employees.

```sql
SELECT e.emp_name,
       d.dept_name
FROM employees e
RIGHT JOIN departments d
ON e.dept_id = d.dept_id;
```

## Question 5
Display a list of employees who do not belong to any department, even if the department data is missing.

```sql
SELECT e.emp_name
FROM employees e
LEFT JOIN departments d
ON e.dept_id = d.dept_id
WHERE d.dept_id IS NULL;
```

## Question 6
Fetch the names of employees and the projects they are assigned to. For employees who are not assigned any projects, show NULL for the project.

```sql
SELECT e.emp_name,
       p.project_name
FROM employees e
LEFT JOIN projects p
ON e.emp_id = p.emp_id;
```

## Question 7
List all employees who have completed at least one project, showing their names and the project names.

```sql
SELECT e.emp_name,
       p.project_name
FROM employees e
INNER JOIN projects p
ON e.emp_id = p.emp_id;
```

## Question 8
Show the names of employees and their projects, ensuring that no project is omitted even if an employee is not assigned to it.

```sql
SELECT e.emp_name,
       p.project_name
FROM employees e
RIGHT JOIN projects p
ON e.emp_id = p.emp_id;
```

## Question 9
Find all employees and their corresponding salaries, and display NULL for salary if there is no salary record for the employee.

```sql
SELECT e.emp_name,
       s.salary
FROM employees e
LEFT JOIN salary s
ON e.emp_id = s.emp_id;
```

## Question 10
Retrieve the names of employees and their corresponding department names, including employees who are not in any department.

```sql
SELECT e.emp_name,
       d.dept_name
FROM employees e
LEFT JOIN departments d
ON e.dept_id = d.dept_id;
```

 ## Question 11
Find the names of all departments and employees, ensuring that departments with no employees are included.

```sql
SELECT d.dept_name,
       e.emp_name
FROM departments d
LEFT JOIN employees e
ON d.dept_id = e.dept_id;
```

## Question 12
List all employees with their contact information, including employees without contact records.

```sql
SELECT e.emp_name,
       c.contact_no
FROM employees e
LEFT JOIN contacts c
ON e.emp_id = c.emp_id;
```

## Question 13
Show the names of employees and their department names, including employees not assigned to any department and departments without employees.

```sql
SELECT e.emp_name,
       d.dept_name
FROM employees e
FULL OUTER JOIN departments d
ON e.dept_id = d.dept_id;
```

## Question 14
Find employees who have not completed any project, along with the project details where applicable.

```sql
SELECT e.emp_name,
       p.project_name
FROM employees e
LEFT JOIN projects p
ON e.emp_id = p.emp_id
WHERE p.project_id IS NULL;
```

## Question 15
Retrieve the names of employees and the names of their projects, including employees who are not working on any project.

```sql
SELECT e.emp_name,
       p.project_name
FROM employees e
LEFT JOIN projects p
ON e.emp_id = p.emp_id;
```

## Question 16
List all projects and the employees assigned to them, even for projects that have no employees.

```sql
SELECT p.project_name,
       e.emp_name
FROM projects p
LEFT JOIN employees e
ON p.emp_id = e.emp_id;
```

## Question 17
Show the names of all employees who have both a manager and at least one project, listing the manager's name as well.

```sql
SELECT e.emp_name,
       m.emp_name AS manager_name,
       p.project_name
FROM employees e
INNER JOIN employees m
ON e.manager_id = m.emp_id
INNER JOIN projects p
ON e.emp_id = p.emp_id;
```

## Question 18
List the names of employees and the corresponding department names, but exclude those employees who don't belong to a department.

```sql
SELECT e.emp_name,
       d.dept_name
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id;
```

## Question 19
Display employees who belong to multiple departments, showing the employee's name and the department names.

```sql
SELECT e.emp_name,
       d.dept_name
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id;
```

## Question 20
List the names of all departments and employees, ensuring that even if a department has no employees, it is included.

```sql
SELECT d.dept_name,
       e.emp_name
FROM departments d
LEFT JOIN employees e
ON d.dept_id = e.dept_id;
```
## Question 21
Retrieve employees who have worked on at least one project and do not belong to a department, listing their name and project details.

```sql
SELECT e.emp_name,
       p.project_name
FROM employees e
INNER JOIN projects p
ON e.emp_id = p.emp_id
WHERE e.dept_id IS NULL;
```

## Question 22
Find the total number of employees who belong to a department, ensuring the departments with no employees are still included.

```sql
SELECT d.dept_name,
       COUNT(e.emp_id) AS total_employees
FROM departments d
LEFT JOIN employees e
ON d.dept_id = e.dept_id
GROUP BY d.dept_name;
```

## Question 23
Show the employees and their managers, displaying only those employees who report to a manager, excluding employees without managers.

```sql
SELECT e.emp_name,
       m.emp_name AS manager_name
FROM employees e
INNER JOIN employees m
ON e.manager_id = m.emp_id;
```

## Question 24
Display all employee names along with their corresponding managers' names, but include employees who do not have managers.

```sql
SELECT e.emp_name,
       m.emp_name AS manager_name
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.emp_id;
```

## Question 25
Find the names of departments and the number of employees in each department, including departments that have no employees.

```sql
SELECT d.dept_name,
       COUNT(e.emp_id) AS employee_count
FROM departments d
LEFT JOIN employees e
ON d.dept_id = e.dept_id
GROUP BY d.dept_name;
```

## Question 26
List all employees and the departments they belong to, ensuring that departments with no employees are also listed.

```sql
SELECT e.emp_name,
       d.dept_name
FROM departments d
LEFT JOIN employees e
ON d.dept_id = e.dept_id;
```

## Question 27
Show a list of employees who do not have any corresponding salary records, along with their names.

```sql
SELECT e.emp_name
FROM employees e
LEFT JOIN salary s
ON e.emp_id = s.emp_id
WHERE s.emp_id IS NULL;
```

## Question 28
Retrieve the names of employees and their project assignments, including employees who are not assigned to any projects.

```sql
SELECT e.emp_name,
       p.project_name
FROM employees e
LEFT JOIN projects p
ON e.emp_id = p.emp_id;
```

## Question 29
List the names of all employees and their respective department and project assignments, including employees who are not assigned to a project or department.

```sql
SELECT e.emp_name,
       d.dept_name,
       p.project_name
FROM employees e
LEFT JOIN departments d
ON e.dept_id = d.dept_id
LEFT JOIN projects p
ON e.emp_id = p.emp_id;
```

## Question 30
Display the names of employees who belong to at least one department, with the department name listed, but include employees without a department as well.

```sql
SELECT e.emp_name,
       d.dept_name
FROM employees e
LEFT JOIN departments d
ON e.dept_id = d.dept_id;
```        
         
         
         
         
