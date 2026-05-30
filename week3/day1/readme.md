                             Joins.docxs
-- 1. Employees and their managers (including employees without managers)
SELECT e.emp_name AS Employee, m.emp_name AS Manager
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.emp_id;

-- 2. All employees and their departments
SELECT e.emp_name, d.dept_name
FROM employees e
LEFT JOIN departments d
ON e.dept_id = d.dept_id;

-- 3. Employees who report to a manager
SELECT e.emp_name AS Employee, m.emp_name AS Manager
FROM employees e
INNER JOIN employees m
ON e.manager_id = m.emp_id;

-- 4. Employees and their departments (including departments without employees)
SELECT e.emp_name, d.dept_name
FROM employees e
RIGHT JOIN departments d
ON e.dept_id = d.dept_id;

-- 5. Employees without departments
SELECT e.emp_name
FROM employees e
LEFT JOIN departments d
ON e.dept_id = d.dept_id
WHERE d.dept_id IS NULL;

-- 6. Employees and projects (including employees without projects)
SELECT e.emp_name, p.project_name
FROM employees e
LEFT JOIN projects p
ON e.emp_id = p.emp_id;

-- 7. Employees who completed at least one project
SELECT e.emp_name, p.project_name
FROM employees e
INNER JOIN projects p
ON e.emp_id = p.emp_id;

-- 8. Employees and projects, no project omitted
SELECT e.emp_name, p.project_name
FROM employees e
RIGHT JOIN projects p
ON e.emp_id = p.emp_id;

-- 9. Employees and salary records
SELECT e.emp_name, s.salary
FROM employees e
LEFT JOIN salary s
ON e.emp_id = s.emp_id;

-- 10. Employees and department names
SELECT e.emp_name, d.dept_name
FROM employees e
LEFT JOIN departments d
ON e.dept_id = d.dept_id;

-- 11. Departments and employees (including departments without employees)
SELECT d.dept_name, e.emp_name
FROM departments d
LEFT JOIN employees e
ON d.dept_id = e.dept_id;

-- 12. Employees and contact information
SELECT e.emp_name, c.contact_no
FROM employees e
LEFT JOIN contacts c
ON e.emp_id = c.emp_id;

-- 13. Employees and departments including unmatched records
SELECT e.emp_name, d.dept_name
FROM employees e
FULL OUTER JOIN departments d
ON e.dept_id = d.dept_id;

-- 14. Employees who have not completed any project
SELECT e.emp_name, p.project_name
FROM employees e
LEFT JOIN projects p
ON e.emp_id = p.emp_id
WHERE p.project_id IS NULL;

-- 15. Employees and project names
SELECT e.emp_name, p.project_name
FROM employees e
LEFT JOIN projects p
ON e.emp_id = p.emp_id;

-- 16. Projects and employees assigned to them
SELECT p.project_name, e.emp_name
FROM projects p
LEFT JOIN employees e
ON p.emp_id = e.emp_id;

-- 17. Employees having manager and at least one project
SELECT e.emp_name, m.emp_name AS manager_name, p.project_name
FROM employees e
INNER JOIN employees m
ON e.manager_id = m.emp_id
INNER JOIN projects p
ON e.emp_id = p.emp_id;

-- 18. Employees with departments only
SELECT e.emp_name, d.dept_name
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id;

-- 19. Employees belonging to departments
SELECT e.emp_name, d.dept_name
FROM employees e
INNER JOIN departments d
ON e.dept_id = d.dept_id;

-- 20. Departments and employees including empty departments
SELECT d.dept_name, e.emp_name
FROM departments d
LEFT JOIN employees e
ON d.dept_id = e.dept_id;

-- 21. Employees with projects but no department
SELECT e.emp_name, p.project_name
FROM employees e
INNER JOIN projects p
ON e.emp_id = p.emp_id
WHERE e.dept_id IS NULL;

-- 22. Number of employees in each department
SELECT d.dept_name, COUNT(e.emp_id) AS total_employees
FROM departments d
LEFT JOIN employees e
ON d.dept_id = e.dept_id
GROUP BY d.dept_name;

-- 23. Employees reporting to a manager
SELECT e.emp_name, m.emp_name AS manager_name
FROM employees e
INNER JOIN employees m
ON e.manager_id = m.emp_id;

-- 24. All employees and managers
SELECT e.emp_name, m.emp_name AS manager_name
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.emp_id;

-- 25. Departments and employee count
SELECT d.dept_name, COUNT(e.emp_id) AS employee_count
FROM departments d
LEFT JOIN employees e
ON d.dept_id = e.dept_id
GROUP BY d.dept_name;

-- 26. Employees and departments including empty departments
SELECT e.emp_name, d.dept_name
FROM departments d
LEFT JOIN employees e
ON d.dept_id = e.dept_id;

-- 27. Employees without salary records
SELECT e.emp_name
FROM employees e
LEFT JOIN salary s
ON e.emp_id = s.emp_id
WHERE s.emp_id IS NULL;

-- 28. Employees and project assignments
SELECT e.emp_name, p.project_name
FROM employees e
LEFT JOIN projects p
ON e.emp_id = p.emp_id;

-- 29. Employees with department and project assignments
SELECT e.emp_name, d.dept_name, p.project_name
FROM employees e
LEFT JOIN departments d
ON e.dept_id = d.dept_id
LEFT JOIN projects p
ON e.emp_id = p.emp_id;

-- 30. Employees with department name, including employees without department
SELECT e.emp_name, d.dept_name
FROM employees e
LEFT JOIN departments d
ON e.dept_id = d.dept_id;
