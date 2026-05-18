## 16. Find staff members earning more than the average salary of their department.

```sql
SELECT st.staff_name, st.salary
FROM Staff st
WHERE st.salary > (
    SELECT AVG(salary)
    FROM Staff
    WHERE department_id = st.department_id
);
```

---

## 17. Display the second highest salary among staff members.

```sql
SELECT MAX(salary) AS second_highest_salary
FROM Staff
WHERE salary < (
    SELECT MAX(salary)
    FROM Staff
);
```

---

## 18. Find students who scored the highest marks in each subject.

```sql
SELECT s.student_name, sub.subject_name, m.marks
FROM Student s
JOIN Mark m
ON s.student_id = m.student_id
JOIN Subject sub
ON m.subject_id = sub.subject_id
WHERE m.marks = (
    SELECT MAX(m2.marks)
    FROM Mark m2
    WHERE m2.subject_id = m.subject_id
);
```

---

## 19. Display all students and their marks, including students without marks.

```sql
SELECT s.student_name, m.marks
FROM Student s
LEFT JOIN Mark m
ON s.student_id = m.student_id;
```

---

## 20. Find subjects where the average marks are below 70.

```sql
SELECT sub.subject_name, AVG(m.marks) AS average_marks
FROM Subject sub
JOIN Mark m
ON sub.subject_id = m.subject_id
GROUP BY sub.subject_name
HAVING AVG(m.marks) < 70;
```

---

## 21. Display students ordered by CGPA in descending order.

```sql
SELECT student_name, cgpa
FROM Student
ORDER BY cgpa DESC;
```

---

## 22. Find the total salary expenditure department-wise.

```sql
SELECT d.department_name, SUM(st.salary) AS total_salary
FROM Department d
LEFT JOIN Staff st
ON d.department_id = st.department_id
GROUP BY d.department_name;
```

---

## 23. Display departments where the total salary exceeds 200000.

```sql
SELECT d.department_name, SUM(st.salary) AS total_salary
FROM Department d
JOIN Staff st
ON d.department_id = st.department_id
GROUP BY d.department_name
HAVING SUM(st.salary) > 200000;
```

---

## 24. Find students admitted after 2021 and having CGPA above 7.5.

```sql
SELECT student_name, admission_year, cgpa
FROM Student
WHERE admission_year > 2021
AND cgpa > 7.5;
```

---

## 25. Display the number of students admitted each year.

```sql
SELECT admission_year, COUNT(student_id) AS total_students
FROM Student
GROUP BY admission_year;
```

---

## 26. Find the city with the maximum number of students.

```sql
SELECT city, COUNT(student_id) AS total_students
FROM Student
GROUP BY city
ORDER BY total_students DESC
LIMIT 1;
```

---

## 27. Display all departments and their staff count, including empty departments.

```sql
SELECT d.department_name, COUNT(st.staff_id) AS staff_count
FROM Department d
LEFT JOIN Staff st
ON d.department_id = st.department_id
GROUP BY d.department_name;
```

---

## 28. Find students who have failed in at least one subject (marks < 50).

```sql
SELECT DISTINCT s.student_name, m.marks
FROM Student s
JOIN Mark m
ON s.student_id = m.student_id
WHERE m.marks < 50;
```

---

## 29. Display staff hired before 2018.

```sql
SELECT staff_name, hire_date
FROM Staff
WHERE hire_date < '2018-01-01';
```

---

## 30. Find departments where no staff salary is recorded as NULL.

```sql
SELECT d.department_name
FROM Department d
JOIN Staff st
ON d.department_id = st.department_id
GROUP BY d.department_name
HAVING COUNT(CASE WHEN st.salary IS NULL THEN 1 END) = 0;
```



## 31. Assign a row number to students ordered by CGPA.

```sql
SELECT student_name, cgpa,
ROW_NUMBER() OVER (ORDER BY cgpa DESC) AS row_num
FROM Student;
```

---

## 32. Rank students based on their CGPA.

```sql
SELECT student_name, cgpa,
RANK() OVER (ORDER BY cgpa DESC) AS student_rank
FROM Student;
```

---

## 33. Display dense rank of staff salaries.

```sql
SELECT staff_name, salary,
DENSE_RANK() OVER (ORDER BY salary DESC) AS salary_rank
FROM Staff;
```

---

## 34. Find the top 3 highest scoring students using window functions.

```sql
SELECT *
FROM (
    SELECT s.student_name,
           SUM(m.marks) AS total_marks,
           DENSE_RANK() OVER (ORDER BY SUM(m.marks) DESC) AS rank_num
    FROM Student s
    JOIN Mark m
    ON s.student_id = m.student_id
    GROUP BY s.student_name
) ranked_students
WHERE rank_num <= 3;
```

---

## 35. Display running total of marks for each student.

```sql
SELECT s.student_name,
       m.exam_date,
       m.marks,
       SUM(m.marks) OVER (
           PARTITION BY s.student_name
           ORDER BY m.exam_date
       ) AS running_total
FROM Student s
JOIN Mark m
ON s.student_id = m.student_id;
```

---

## 36. Find the average marks for each subject using window functions.

```sql
SELECT sub.subject_name,
       m.marks,
       AVG(m.marks) OVER (
           PARTITION BY sub.subject_name
       ) AS average_marks
FROM Subject sub
JOIN Mark m
ON sub.subject_id = m.subject_id;
```

---

## 37. Display previous exam marks for each student using LAG().

```sql
SELECT s.student_name,
       m.exam_date,
       m.marks,
       LAG(m.marks) OVER (
           PARTITION BY s.student_name
           ORDER BY m.exam_date
       ) AS previous_marks
FROM Student s
JOIN Mark m
ON s.student_id = m.student_id;
```

---

## 38. Display next exam marks for each student using LEAD().

```sql
SELECT s.student_name,
       m.exam_date,
       m.marks,
       LEAD(m.marks) OVER (
           PARTITION BY s.student_name
           ORDER BY m.exam_date
       ) AS next_marks
FROM Student s
JOIN Mark m
ON s.student_id = m.student_id;
```

---

## 39. Find the highest marks within each subject using MAX() OVER().

```sql
SELECT sub.subject_name,
       m.marks,
       MAX(m.marks) OVER (
           PARTITION BY sub.subject_name
       ) AS highest_marks
FROM Subject sub
JOIN Mark m
ON sub.subject_id = m.subject_id;
```

---

## 40. Display cumulative average marks ordered by exam date.

```sql
SELECT exam_date,
       marks,
       AVG(marks) OVER (
           ORDER BY exam_date
       ) AS cumulative_average
FROM Mark;
```

---

## 41. Find the first student admitted in each department.

```sql
SELECT *
FROM (
    SELECT s.student_name,
           d.department_name,
           s.admission_year,
           ROW_NUMBER() OVER (
               PARTITION BY d.department_name
               ORDER BY s.admission_year
           ) AS row_num
    FROM Student s
    JOIN Department d
    ON s.department_id = d.department_id
) ranked_students
WHERE row_num = 1;
```

---

## 42. Display the latest hired staff member in each department.

```sql
SELECT *
FROM (
    SELECT st.staff_name,
           d.department_name,
           st.hire_date,
           ROW_NUMBER() OVER (
               PARTITION BY d.department_name
               ORDER BY st.hire_date DESC
           ) AS row_num
    FROM Staff st
    JOIN Department d
    ON st.department_id = d.department_id
) ranked_staff
WHERE row_num = 1;
```

---

## 43. Divide students into 4 CGPA quartiles using NTILE().

```sql
SELECT student_name,
       cgpa,
       NTILE(4) OVER (
           ORDER BY cgpa DESC
       ) AS quartile
FROM Student;
```

---

## 44. Find percentage rank of students based on CGPA.

```sql
SELECT student_name,
       cgpa,
       PERCENT_RANK() OVER (
           ORDER BY cgpa
       ) AS percentage_rank
FROM Student;
```

---

## 45. Display cumulative distribution of salaries.

```sql
SELECT staff_name,
       salary,
       CUME_DIST() OVER (
           ORDER BY salary
       ) AS cumulative_distribution
FROM Staff;
```
