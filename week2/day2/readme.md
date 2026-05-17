DAY 2 – SQL WINDOW FUNCTIONS

Theory

ROW_NUMBER() -> Assigns unique row numbers

RANK() -> Ranking with gaps

DENSE_RANK() -> Ranking without gaps

PARTITION BY -> Divides rows into groups

LAG() -> Returns previous row value

LEAD() -> Returns next row value

--------------------------------------------------

1. ROW_NUMBER()

SELECT employee_name,
       salary,
       ROW_NUMBER() OVER(ORDER BY salary DESC) AS row_num
FROM employees;

--------------------------------------------------

2. RANK()

SELECT employee_name,
       salary,
       RANK() OVER(ORDER BY salary DESC) AS rank_num
FROM employees;

--------------------------------------------------

3. DENSE_RANK()

SELECT employee_name,
       salary,
       DENSE_RANK() OVER(ORDER BY salary DESC) AS dense_rank_num
FROM employees;

--------------------------------------------------

4. Top 3 highest-paid employees

SELECT *
FROM (
    SELECT employee_name,
           salary,
           ROW_NUMBER() OVER(ORDER BY salary DESC) AS rn
    FROM employees
) t
WHERE rn <= 3;

--------------------------------------------------

5. Rank employees within departments

SELECT employee_name,
       department,
       salary,
       RANK() OVER(PARTITION BY department ORDER BY salary DESC) AS dept_rank
FROM employees;

--------------------------------------------------

6. Highest salary in each department

SELECT employee_name,
       department,
       salary,
       MAX(salary) OVER(PARTITION BY department) AS highest_salary
FROM employees;

--------------------------------------------------

7. Running total of order amounts

SELECT order_id,
       order_date,
       total_amount,
       SUM(total_amount) OVER(ORDER BY order_date) AS running_total
FROM orders;

--------------------------------------------------

8. Cumulative sales amount for each employee

SELECT employee_id,
       total_amount,
       SUM(total_amount) OVER(PARTITION BY employee_id) AS total_sales
FROM orders;

--------------------------------------------------

9. LAG() example

SELECT customer_id,
       order_date,
       total_amount,
       LAG(total_amount) OVER(PARTITION BY customer_id ORDER BY order_date) AS previous_order
FROM orders;

--------------------------------------------------

10. LEAD() example

SELECT customer_id,
       order_date,
       total_amount,
       LEAD(total_amount) OVER(PARTITION BY customer_id ORDER BY order_date) AS next_order
FROM orders;
