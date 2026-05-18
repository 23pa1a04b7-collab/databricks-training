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









##LEFT JOIN

LEFT JOIN returns all records from the left table and matching records from the right table. If there is no match, NULL values
''sql

 1.SELECT *
FROM table1
LEFT JOIN table2
ON table1.id = table2.id;


RIGHT JOIN

RIGHT JOIN returns all records from the right table and matching records from the left table.

  2.SELECT *
FROM table1
RIGHT JOIN table2
ON table1.id = table2.id;

FULL OUTER JOIN

FULL OUTER JOIN returns all matching and non-matching rows from both tables.

SELECT *
FROM table1
FULL OUTER JOIN table2
ON table1.id = table2.id;

1. Display all students and the courses they are enrolled in.
 SELECT s.student_name, c.course_name
FROM students s
LEFT JOIN enrollments e
ON s.student_id = e.student_id
LEFT JOIN courses c
ON e.course_id = c.course_id;

2. Find all courses that currently have no students enrolled.

SELECT c.course_name
FROM courses c
LEFT JOIN enrollments e
ON c.course_id = e.course_id
WHERE e.student_id IS NULL;

4. Find all courses without instructors.

SELECT course_name
FROM courses
WHERE instructor_id IS NULL;

5. Display students and enrollment information using RIGHT JOIN.
SELECT s.student_name, e.course_id
FROM students s
RIGHT JOIN enrollments e
ON s.student_id = e.student_id;

6.Find students not enrolled in any course.
SELECT s.student_name
FROM students s
LEFT JOIN enrollments e
ON s.student_id = e.student_id
WHERE e.course_id IS NULL;

7. FULL OUTER JOIN for students and enrollments.
SELECT s.student_name, e.course_id
FROM students s
FULL OUTER JOIN enrollments e
ON s.student_id = e.student_id;

8. Find courses never appearing in enrollments.

SELECT c.course_name
FROM courses c
LEFT JOIN enrollments e
ON c.course_id = e.course_id
WHERE e.course_id IS NULL;

9. FULL OUTER JOIN for instructors and courses.
 SELECT i.instructor_name, c.course_name
FROM instructors i
FULL OUTER JOIN courses c
ON i.instructor_id = c.instructor_id;


10. Report showing student, course, and instructor names.
SELECT s.student_name,
       c.course_name,
       i.instructor_name
FROM students s
LEFT JOIN enrollments e
ON s.student_id = e.student_id
LEFT JOIN courses c
ON e.course_id = c.course_id


Bonus Challenge
SELECT s.student_name, c.course_name
FROM students s
CROSS JOIN courses c;
LEFT JOIN instructors i
ON c.instructor_id = i.instructor_id;











CROSS JOIN courses c;

