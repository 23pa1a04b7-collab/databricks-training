DAY 2 – SQL WINDOW FUNCTIONS

Theory

ROW_NUMBER() -> Assigns unique row numbers

RANK() -> Ranking with gaps

DENSE_RANK() -> Ranking without gaps

PARTITION BY -> Divides rows into groups

LAG() -> Returns previous row value

LEAD() -> Returns next row value

--------------------------------------------------
###Database Schema
The datasets models a retail sales company with employees,customers,products,and orders.

### 1.employees
employee_id        employee_name      department       salary       hire_date
1                  Alice johnson      sales            70000         2020-01-15
2                  Bob Smith          sales            65000         2021-03-20
3                 Charlie Brown        IT              90000         2019-07-01
4                 Diana Prince         IT              95000         2018-11-11



##  2.orders
order_id           customer_id         employee_id      order_date      total_amount
101                 1                   1               2024-01-10       500
102                 2                   2               2024-01-11       700
103                 1                   1                2024-01-15       1200
104                 3                   3                 2024-01-18       300



















# DAY 2 – SQL WINDOW FUNCTIONS

## 1. Use ROW_NUMBER() to assign a row number to employees ordered by salary descending.

```sql
SELECT employee_name,
       salary,
       ROW_NUMBER() OVER(ORDER BY salary DESC) AS row_num
FROM employees;
```

---

## 2. Use RANK() to rank employees by salary.

```sql
SELECT employee_name,
       salary,
       RANK() OVER(ORDER BY salary DESC) AS rank_num
FROM employees;
```

---

## 3. Use DENSE_RANK() to rank employees by salary.

```sql
SELECT employee_name,
       salary,
       DENSE_RANK() OVER(ORDER BY salary DESC) AS dense_rank_num
FROM employees;
```

---

## 4. Find the top 3 highest-paid employees.

```sql
SELECT *
FROM (
    SELECT employee_name,
           salary,
           ROW_NUMBER() OVER(ORDER BY salary DESC) AS rn
    FROM employees
) t
WHERE rn <= 3;
```

---

## 5. Rank employees within each department using PARTITION BY.

```sql
SELECT employee_name,
       department,
       salary,
       RANK() OVER(PARTITION BY department ORDER BY salary DESC) AS dept_rank
FROM employees;
```

---

## 6. Display the highest salary in each department.

```sql
SELECT employee_name,
       department,
       salary,
       MAX(salary) OVER(PARTITION BY department) AS highest_salary
FROM employees;
```

---

## 7. Calculate the running total of order amounts ordered by order_date.

```sql
SELECT order_id,
       order_date,
       total_amount,
       SUM(total_amount) OVER(ORDER BY order_date) AS running_total
FROM orders;
```

---

## 8. Calculate the cumulative sales amount for each employee.

```sql
SELECT employee_id,
       total_amount,
       SUM(total_amount) OVER(PARTITION BY employee_id) AS total_sales
FROM orders;
```

---

## 9. Use LAG() to show the previous order amount for each customer.

```sql
SELECT customer_id,
       order_date,
       total_amount,
       LAG(total_amount) OVER(PARTITION BY customer_id ORDER BY order_date) AS previous_order
FROM orders;
```

---

## 10. Use LEAD() to show the next order amount for each customer.

```sql
SELECT customer_id,
       order_date,
       total_amount,
       LEAD(total_amount) OVER(PARTITION BY customer_id ORDER BY order_date) AS next_order
FROM orders;
```

---

## 11. Find the difference between current and previous order amount.

```sql
SELECT customer_id,
       total_amount,
       total_amount - LAG(total_amount) OVER(PARTITION BY customer_id ORDER BY order_date) AS difference
FROM orders;
```

---

## 12. Calculate moving average of the last 3 orders.

```sql
SELECT order_id,
       total_amount,
       AVG(total_amount) OVER(
           ORDER BY order_date
           ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
       ) AS moving_avg
FROM orders;
```

---

## 13. Use NTILE(4) to divide employees into salary quartiles.

```sql
SELECT employee_name,
       salary,
       NTILE(4) OVER(ORDER BY salary DESC) AS quartile
FROM employees;
```

---

## 14. Find the first order placed by each customer.

```sql
SELECT *
FROM (
    SELECT *,
           ROW_NUMBER() OVER(PARTITION BY customer_id ORDER BY order_date) AS rn
    FROM orders
) t
WHERE rn = 1;
```

---

## 15. Find the latest order placed by each customer.

```sql
SELECT *
FROM (
    SELECT *,
           ROW_NUMBER() OVER(PARTITION BY customer_id ORDER BY order_date DESC) AS rn
    FROM orders
) t
WHERE rn = 1;
```

---

## 16. Display employee salaries along with department average salary.

```sql
SELECT employee_name,
       department,
       salary,
       AVG(salary) OVER(PARTITION BY department) AS dept_avg_salary
FROM employees;
```

---

## 17. Find employees earning above their department average salary.

```sql
SELECT *
FROM (
    SELECT employee_name,
           department,
           salary,
           AVG(salary) OVER(PARTITION BY department) AS avg_salary
    FROM employees
) t
WHERE salary > avg_salary;
```

---

## 18. Use SUM() OVER(PARTITION BY department) to calculate department payroll.

```sql
SELECT employee_name,
       department,
       salary,
       SUM(salary) OVER(PARTITION BY department) AS department_payroll
FROM employees;
```

---

## 19. Find the percentage contribution of each employee salary within their department.

```sql
SELECT employee_name,
       department,
       salary,
       ROUND(
           salary * 100.0 /
           SUM(salary) OVER(PARTITION BY department),
           2
       ) AS percentage_contribution
FROM employees;
```

---

## 20. Use COUNT() OVER() to show total number of employees alongside each row.

```sql
SELECT employee_name,
       COUNT(*) OVER() AS total_employees
FROM employees;
```

---

## 21. Create a CTE to calculate total sales per employee.

```sql
WITH sales_cte AS (
    SELECT employee_id,
           SUM(total_amount) AS total_sales
    FROM orders
    GROUP BY employee_id
)
SELECT *
FROM sales_cte;
```

---

## 22. Use a CTE to find employees whose sales exceed the company average.

```sql
WITH sales_cte AS (
    SELECT employee_id,
           SUM(total_amount) AS total_sales
    FROM orders
    GROUP BY employee_id
)
SELECT *
FROM sales_cte
WHERE total_sales > (
    SELECT AVG(total_sales)
    FROM sales_cte
);
```

---

## 23. Create multiple CTEs to calculate customer total spending and rankings.

```sql
WITH customer_totals AS (
    SELECT customer_id,
           SUM(total_amount) AS total_spending
    FROM orders
    GROUP BY customer_id
),
customer_ranks AS (
    SELECT customer_id,
           total_spending,
           RANK() OVER(ORDER BY total_spending DESC) AS ranking
    FROM customer_totals
)
SELECT *
FROM customer_ranks;
```

---

## 24. Write a recursive CTE to generate numbers from 1 to 10.

```sql
WITH RECURSIVE numbers AS (
    SELECT 1 AS n
    UNION ALL
    SELECT n + 1
    FROM numbers
    WHERE n < 10
)
SELECT *
FROM numbers;
```

---

## 25. Use a recursive CTE to display employee hierarchy data.

```sql
WITH RECURSIVE employee_hierarchy AS (
    SELECT employee_id,
           employee_name,
           manager_id
    FROM employees
    WHERE manager_id IS NULL

    UNION ALL

    SELECT e.employee_id,
           e.employee_name,
           e.manager_id
    FROM employees e
    JOIN employee_hierarchy eh
    ON e.manager_id = eh.employee_id
)
SELECT *
FROM employee_hierarchy;
```

---

## 26. Create a CTE that filters orders above the average order amount.

```sql
WITH avg_order AS (
    SELECT AVG(total_amount) AS avg_amount
    FROM orders
)
SELECT *
FROM orders
WHERE total_amount > (
    SELECT avg_amount
    FROM avg_order
);
```

---

## 27. Use a CTE and window function together to rank customers by total spending.

```sql
WITH customer_totals AS (
    SELECT customer_id,
           SUM(total_amount) AS total_spending
    FROM orders
    GROUP BY customer_id
)
SELECT customer_id,
       total_spending,
       RANK() OVER(ORDER BY total_spending DESC) AS customer_rank
FROM customer_totals;
```

---

## 28. Find the second-highest salary in each department.

```sql
SELECT *
FROM (
    SELECT employee_name,
           department,
           salary,
           DENSE_RANK() OVER(PARTITION BY department ORDER BY salary DESC) AS salary_rank
    FROM employees
) t
WHERE salary_rank = 2;
```

---

## 29. Display the difference between each employee salary and department maximum salary.

```sql
SELECT employee_name,
       department,
       salary,
       MAX(salary) OVER(PARTITION BY department) - salary AS salary_difference
FROM employees;
```

---

## 30. Combine CTEs and window functions to find the top-performing employee in each department based on sales.

```sql
WITH employee_sales AS (
    SELECT e.employee_id,
           e.employee_name,
           e.department,
           SUM(o.total_amount) AS total_sales
    FROM employees e
    JOIN orders o
    ON e.employee_id = o.employee_id
    GROUP BY e.employee_id, e.employee_name, e.department
)
SELECT *
FROM (
    SELECT *,
           RANK() OVER(PARTITION BY department ORDER BY total_sales DESC) AS dept_rank
    FROM employee_sales
) t
WHERE dept_rank = 1;
```
