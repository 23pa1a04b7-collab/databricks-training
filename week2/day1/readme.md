DAY 1 – SQL JOINS

Theory

LEFT JOIN:
Returns all rows from left table and matching rows from right table.

RIGHT JOIN:
Returns all rows from right table and matching rows from left table.

FULL OUTER JOIN:
Returns all matching and non-matching rows from both tables.

--------------------------------------------------

1. Display all students and the courses they are enrolled in.

SELECT s.student_name, c.course_name
FROM students s
LEFT JOIN enrollments e
ON s.student_id = e.student_id
LEFT JOIN courses c
ON e.course_id = c.course_id;

--------------------------------------------------

2. Find all courses that currently have no students enrolled.

SELECT c.course_name
FROM courses c
LEFT JOIN enrollments e
ON c.course_id = e.course_id
WHERE e.student_id IS NULL;

--------------------------------------------------

3. Display all instructors and the courses they teach.

SELECT i.instructor_name, c.course_name
FROM instructors i
LEFT JOIN courses c
ON i.instructor_id = c.instructor_id;

--------------------------------------------------

4. Find all courses without instructors.

SELECT course_name
FROM courses
WHERE instructor_id IS NULL;

--------------------------------------------------

5. Display students and enrollment information using RIGHT JOIN.

SELECT s.student_name, e.course_id
FROM students s
RIGHT JOIN enrollments e
ON s.student_id = e.student_id;

--------------------------------------------------

6. Find students not enrolled in any course.

SELECT s.student_name
FROM students s
LEFT JOIN enrollments e
ON s.student_id = e.student_id
WHERE e.course_id IS NULL;

--------------------------------------------------

7. FULL OUTER JOIN for students and enrollments.

SELECT s.student_name, e.course_id
FROM students s
FULL OUTER JOIN enrollments e
ON s.student_id = e.student_id;

--------------------------------------------------

8. Find courses never appearing in enrollments.

SELECT c.course_name
FROM courses c
LEFT JOIN enrollments e
ON c.course_id = e.course_id
WHERE e.course_id IS NULL;

--------------------------------------------------

9. FULL OUTER JOIN for instructors and courses.

SELECT i.instructor_name, c.course_name
FROM instructors i
FULL OUTER JOIN courses c
ON i.instructor_id = c.instructor_id;

--------------------------------------------------

10. Report showing student, course, and instructor names.

SELECT s.student_name,
       c.course_name,
       i.instructor_name
FROM students s
LEFT JOIN enrollments e
ON s.student_id = e.student_id
LEFT JOIN courses c
ON e.course_id = c.course_id
LEFT JOIN instructors i
ON c.instructor_id = i.instructor_id;

--------------------------------------------------

Bonus Challenge

SELECT s.student_name, c.course_name
FROM students s
CROSS JOIN courses c;

