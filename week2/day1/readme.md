DAY 1 – SQL JOINS
Theory
##student
student_id                student_name            email
1.                        Alice johnson           alice@email.com
2.                        Bob Smith               bob@email.com
3.                        Charlie Brown           charlie@email.com
4.                        Diana Prince            diana@email.com
5.                        Ethan Hunt              ethan@email.com

##courses
course_id              course_name             instructor_id
101                    SQL Basics               1
102                    Python Fundamentals      2
103                    Data Analytics           Null
104                    Cloud Computing          3
105                    Machine Learning         Null


# SQL JOINS ASSIGNMENT

## 1. Display all students and the courses they are enrolled in. Include students who are not enrolled in any course.

```sql
SELECT s.student_name, c.course_name
FROM students s
LEFT JOIN enrollments e
ON s.student_id = e.student_id
LEFT JOIN courses c
ON e.course_id = c.course_id;
```

---

## 2. Find all courses that currently have no students enrolled.

```sql
SELECT c.course_name
FROM courses c
LEFT JOIN enrollments e
ON c.course_id = e.course_id
WHERE e.student_id IS NULL;
```

---

## 3. Display all instructors and the courses they teach, including instructors who are not assigned to any course.

```sql
SELECT i.instructor_name, c.course_name
FROM instructors i
LEFT JOIN courses c
ON i.instructor_id = c.instructor_id;
```

---

## 4. Find all courses that do not have an instructor assigned.

```sql
SELECT course_name
FROM courses
WHERE instructor_id IS NULL;
```

---

## 5. Display all students and enrollment information using a RIGHT JOIN.

```sql
SELECT s.student_name, e.course_id
FROM students s
RIGHT JOIN enrollments e
ON s.student_id = e.student_id;
```

---

## 6. Find students who are not enrolled in any course.

```sql
SELECT s.student_name
FROM students s
LEFT JOIN enrollments e
ON s.student_id = e.student_id
WHERE e.course_id IS NULL;
```

---

## 7. Use a FULL OUTER JOIN to display all students and enrollments, including unmatched rows from both tables.

```sql
SELECT s.student_name, e.course_id
FROM students s
FULL OUTER JOIN enrollments e
ON s.student_id = e.student_id;
```

---

## 8. Find all courses that have never appeared in the enrollments table.

```sql
SELECT c.course_name
FROM courses c
LEFT JOIN enrollments e
ON c.course_id = e.course_id
WHERE e.course_id IS NULL;
```

---

## 9. Display all instructors and courses using a FULL OUTER JOIN and identify unmatched rows.

```sql
SELECT i.instructor_name, c.course_name
FROM instructors i
FULL OUTER JOIN courses c
ON i.instructor_id = c.instructor_id;
```

---

## 10. Create a report showing student name, course name, and instructor name. Include rows even if course or instructor information is missing.

```sql
SELECT s.student_name, c.course_name, i.instructor_name
FROM students s
LEFT JOIN enrollments e
ON s.student_id = e.student_id
LEFT JOIN courses c
ON e.course_id = c.course_id
LEFT JOIN instructors i
ON c.instructor_id = i.instructor_id;
```

---

# Bonus Challenge

## Write a query that lists every student and every course, even if there is no enrollment relationship between them.

```sql
SELECT s.student_name, c.course_name
FROM students s
CROSS JOIN courses c;
```




















WHERE instructor_id IS NULL;
```
