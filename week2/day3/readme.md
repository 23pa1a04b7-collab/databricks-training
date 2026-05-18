-- =====================================================
-- COLLEGE MANAGEMENT SYSTEM (CMS)
-- COMPLETE PRACTICE DATABASE
-- =====================================================

DROP TABLE IF EXISTS Mark;
DROP TABLE IF EXISTS Subject;
DROP TABLE IF EXISTS Student;
DROP TABLE IF EXISTS Staff;
DROP TABLE IF EXISTS Department;

CREATE TABLE Department (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50),
    department_block_number INT,
    yearly_budget DECIMAL(12,2)
);

CREATE TABLE Staff (
    staff_id INT PRIMARY KEY,
    staff_name VARCHAR(50),
    designation VARCHAR(30),
    salary DECIMAL(10,2),
    hire_date DATE,
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES Department(department_id)
);

CREATE TABLE Student (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50),
    gender VARCHAR(10),
    city VARCHAR(50),
    admission_year INT,
    department_id INT,
    cgpa DECIMAL(3,2),
    FOREIGN KEY (department_id) REFERENCES Department(department_id)
);

CREATE TABLE Subject (
    subject_id INT PRIMARY KEY,
    subject_name VARCHAR(50),
    subject_code VARCHAR(20),
    semester INT,
    credits INT,
    staff_id INT,
    FOREIGN KEY (staff_id) REFERENCES Staff(staff_id)
);

CREATE TABLE Mark (
    student_id INT,
    subject_id INT,
    exam_type VARCHAR(20),
    marks INT,
    exam_date DATE,
    PRIMARY KEY(student_id, subject_id, exam_type),
    FOREIGN KEY (student_id) REFERENCES Student(student_id),
    FOREIGN KEY (subject_id) REFERENCES Subject(subject_id)
);

-- =====================================================
-- INSERT DEPARTMENTS
-- =====================================================

INSERT INTO Department VALUES
(1,'Computer Science',101,800000),
(2,'Mechanical',102,600000),
(3,'Electronics',103,550000),
(4,'Civil',104,450000),
(5,'Mathematics',105,300000),
(6,NULL,106,200000),
(7,'Biotechnology',NULL,NULL);

-- =====================================================
-- INSERT STAFF
-- =====================================================

INSERT INTO Staff VALUES
(1,'Alice Johnson','Professor',95000,'2015-06-12',1),
(2,'Bob Smith','Associate Professor',82000,'2017-09-01',1),
(3,'Charlie Brown','Professor',91000,'2014-03-21',2),
(4,'David Lee','Lecturer',55000,'2020-07-15',2),
(5,'Eva Green','Professor',99000,'2013-11-05',3),
(6,'Frank Hall','Lecturer',NULL,'2021-01-12',3),
(7,'Grace Miller','HOD',120000,'2010-02-28',4),
(8,NULL,'Lecturer',50000,'2022-08-18',NULL),
(9,'Henry Ford','Assistant Professor',65000,NULL,5),
(10,'Ivy Clark','Professor',98000,'2012-04-17',NULL);

-- =====================================================
-- INSERT STUDENTS
-- =====================================================

INSERT INTO Student VALUES
(101,'John Doe','Male','New York',2021,1,8.7),
(102,'Mary Jane','Female','Chicago',2020,1,9.1),
(103,'Steve Rogers','Male','Dallas',2022,2,7.5),
(104,'Natasha Romanoff','Female','Boston',2021,2,8.0),
(105,'Bruce Wayne','Male','Gotham',2019,3,9.5),
(106,'Clark Kent','Male','Metropolis',2020,3,6.9),
(107,'Diana Prince','Female','Washington',2022,4,8.4),
(108,'Peter Parker','Male','Queens',2021,4,NULL),
(109,'Tony Stark','Male','Malibu',2019,1,9.8),
(110,'Wanda Maximoff','Female','Chicago',2022,5,7.2),
(111,'Barry Allen','Male',NULL,2023,5,6.5),
(112,NULL,'Female','Seattle',2023,NULL,NULL),
(113,'Scott Lang','Male','San Francisco',2021,NULL,5.8),
(114,'Jean Grey','Female','New York',2020,6,8.8),
(115,'Logan Howlett','Male','Denver',2022,7,7.7);

-- =====================================================
-- INSERT SUBJECTS
-- =====================================================

INSERT INTO Subject VALUES
(201,'Database Systems','CS301',3,4,1),
(202,'Operating Systems','CS302',3,4,2),
(203,'Machine Design','ME201',4,3,3),
(204,'Thermodynamics','ME202',4,4,4),
(205,'Digital Electronics','EC301',5,4,5),
(206,'Signals and Systems','EC302',5,3,6),
(207,'Structural Engineering','CV401',6,4,7),
(208,'Linear Algebra','MA101',1,3,9),
(209,NULL,'GEN999',2,2,NULL),
(210,'Artificial Intelligence','CS401',6,5,1);

-- =====================================================
-- INSERT MARKS
-- =====================================================

INSERT INTO Mark VALUES
(101,201,'Mid',88,'2024-03-10'),
(101,201,'Final',91,'2024-05-10'),
(101,202,'Mid',75,'2024-03-11'),
(102,201,'Mid',95,'2024-03-10'),
(102,202,'Final',89,'2024-05-11'),
(103,203,'Mid',66,'2024-03-09'),
(103,204,'Final',72,'2024-05-12'),
(104,203,'Final',81,'2024-05-12'),
(105,205,'Mid',98,'2024-03-14'),
(105,206,'Final',94,'2024-05-14'),
(106,205,'Mid',54,'2024-03-14'),
(106,206,'Final',61,'2024-05-14'),
(107,207,'Mid',87,'2024-03-16'),
(108,207,'Final',NULL,'2024-05-16'),
(109,201,'Final',99,'2024-05-10'),
(109,210,'Mid',97,'2024-03-20'),
(110,208,'Mid',71,'2024-03-18'),
(111,208,'Final',65,'2024-05-18'),
(112,209,'Mid',NULL,'2024-03-21'),
(113,210,'Final',44,'2024-05-20'),
(114,208,'Mid',90,'2024-03-18'),
(115,209,'Final',73,'2024-05-22');


-- 1. List all students along with their department names
SELECT s.student_name, d.department_name
FROM Student s
JOIN Department d
ON s.department_id = d.department_id;

-- 2. Display all staff members and their department names, including staff without departments
SELECT st.staff_name, d.department_name
FROM Staff st
LEFT JOIN Department d
ON st.department_id = d.department_id;

-- 3. Find all departments that currently have no students assigned
SELECT d.department_name
FROM Department d
LEFT JOIN Student s
ON d.department_id = s.department_id
WHERE s.student_id IS NULL;

-- 4. Show students who do not have any marks recorded
SELECT s.student_name
FROM Student s
LEFT JOIN Mark m
ON s.student_id = m.student_id
WHERE m.student_id IS NULL;

-- 5. Display subjects that are not assigned to any staff member
SELECT subject_name
FROM Subject
WHERE staff_id IS NULL;

-- 6. Find the average CGPA department-wise
SELECT d.department_name,
AVG(s.cgpa) AS average_cgpa
FROM Student s
JOIN Department d
ON s.department_id = d.department_id
GROUP BY d.department_name;

-- 7. Display departments where the average CGPA is greater than 8.0
SELECT d.department_name,
AVG(s.cgpa) AS average_cgpa
FROM Student s
JOIN Department d
ON s.department_id = d.department_id
GROUP BY d.department_name
HAVING AVG(s.cgpa) > 8.0;

-- 8. Find the total number of students in each department
SELECT d.department_name,
COUNT(s.student_id) AS total_students
FROM Department d
LEFT JOIN Student s
ON d.department_id = s.department_id
GROUP BY d.department_name;

-- 9. Display the highest and lowest marks scored in each subject
SELECT sub.subject_name,
MAX(m.marks) AS highest_marks,
MIN(m.marks) AS lowest_marks
FROM Mark m
JOIN Subject sub
ON m.subject_id = sub.subject_id
GROUP BY sub.subject_name;

-- 10. Find students who scored more than 90 in any exam
SELECT DISTINCT s.student_name
FROM Student s
JOIN Mark m
ON s.student_id = m.student_id
WHERE m.marks > 90;

-- 11. Display the names of students who belong to the Computer Science department
SELECT s.student_name
FROM Student s
JOIN Department d
ON s.department_id = d.department_id
WHERE d.department_name = 'Computer Science';

-- 12. Find the number of subjects handled by each staff member
SELECT st.staff_name,
COUNT(sub.subject_id) AS total_subjects
FROM Staff st
LEFT JOIN Subject sub
ON st.staff_id = sub.staff_id
GROUP BY st.staff_name;

-- 13. Display students along with the total marks they obtained across all subjects
SELECT s.student_name,
SUM(m.marks) AS total_marks
FROM Student s
LEFT JOIN Mark m
ON s.student_id = m.student_id
GROUP BY s.student_name;

-- 14. Find departments with more than 2 staff members
SELECT d.department_name,
COUNT(st.staff_id) AS total_staff
FROM Department d
JOIN Staff st
ON d.department_id = st.department_id
GROUP BY d.department_name
HAVING COUNT(st.staff_id) > 2;

-- 15. Display students whose CGPA is above the average CGPA
SELECT student_name, cgpa
FROM Student
WHERE cgpa >
(
SELECT AVG(cgpa)
FROM Student
);

-- 16. Find staff members earning more than the average salary of their department
SELECT st.staff_name, st.salary
FROM Staff st
WHERE st.salary >
(
SELECT AVG(salary)
FROM Staff
WHERE department_id = st.department_id
);

-- 17. Display the second highest salary among staff members
SELECT MAX(salary) AS second_highest_salary
FROM Staff
WHERE salary <
(
SELECT MAX(salary)
FROM Staff
);

-- 18. Find students who scored the highest marks in each subject
SELECT s.student_name,
sub.subject_name,
m.marks
FROM Mark m
JOIN Student s
ON m.student_id = s.student_id
JOIN Subject sub
ON m.subject_id = sub.subject_id
WHERE m.marks =
(
SELECT MAX(m2.marks)
FROM Mark m2
WHERE m2.subject_id = m.subject_id
);

-- 19. Display all students and their marks, including students without marks
SELECT s.student_name, m.marks
FROM Student s
LEFT JOIN Mark m
ON s.student_id = m.student_id;

-- 20. Find subjects where the average marks are below 70
SELECT sub.subject_name,
AVG(m.marks) AS average_marks
FROM Mark m
JOIN Subject sub
ON m.subject_id = sub.subject_id
GROUP BY sub.subject_name
HAVING AVG(m.marks) < 70;

-- 21. Display students ordered by CGPA in descending order
SELECT student_name, cgpa
FROM Student
ORDER BY cgpa DESC;

-- 22. Find the total salary expenditure department-wise
SELECT d.department_name,
SUM(st.salary) AS total_salary
FROM Department d
JOIN Staff st
ON d.department_id = st.department_id
GROUP BY d.department_name;

-- 23. Display departments where the total salary exceeds 200000
SELECT d.department_name,
SUM(st.salary) AS total_salary
FROM Department d
JOIN Staff st
ON d.department_id = st.department_id
GROUP BY d.department_name
HAVING SUM(st.salary) > 200000;

-- 24. Find students admitted after 2021 and having CGPA above 7.5
SELECT student_name, admission_year, cgpa
FROM Student
WHERE admission_year > 2021
AND cgpa > 7.5;

-- 25. Display the number of students admitted each year
SELECT admission_year,
COUNT(student_id) AS total_students
FROM Student
GROUP BY admission_year;

-- 26. Find the city with the maximum number of students
SELECT city,
COUNT(student_id) AS total_students
FROM Student
GROUP BY city
ORDER BY total_students DESC
LIMIT 1;

-- 27. Display all departments and their staff count, including empty departments
SELECT d.department_name,
COUNT(st.staff_id) AS total_staff
FROM Department d
LEFT JOIN Staff st
ON d.department_id = st.department_id
GROUP BY d.department_name;

-- 28. Find students who have failed in at least one subject
SELECT DISTINCT s.student_name
FROM Student s
JOIN Mark m
ON s.student_id = m.student_id
WHERE m.marks < 50;

-- 29. Display staff hired before 2018
SELECT staff_name, hire_date
FROM Staff
WHERE YEAR(hire_date) < 2018;

-- 30. Find departments where no staff salary is recorded as NULL
SELECT d.department_name
FROM Department d
JOIN Staff st
ON d.department_id = st.department_id
GROUP BY d.department_name
HAVING COUNT(*) = COUNT(st.salary);

-- 31. Assign a row number to students ordered by CGPA
SELECT student_name,
cgpa,
ROW_NUMBER() OVER (ORDER BY cgpa DESC) AS row_number
FROM Student;

-- 32. Rank students based on their CGPA
SELECT student_name,
cgpa,
RANK() OVER (ORDER BY cgpa DESC) AS student_rank
FROM Student;

-- 33. Display dense rank of staff salaries
SELECT staff_name,
salary,
DENSE_RANK() OVER (ORDER BY salary DESC) AS dense_rank_salary
FROM Staff;

-- 34. Find the top 3 highest scoring students using window functions
SELECT *
FROM
(
SELECT s.student_name,
SUM(m.marks) AS total_marks,
RANK() OVER (ORDER BY SUM(m.marks) DESC) AS rank_number
FROM Student s
JOIN Mark m
ON s.student_id = m.student_id
GROUP BY s.student_name
) t
WHERE rank_number <= 3;

-- 35. Display running total of marks for each student
SELECT student_id,
exam_date,
marks,
SUM(marks) OVER
(
PARTITION BY student_id
ORDER BY exam_date
) AS running_total
FROM Mark;

-- 36. Find the average marks for each subject using window functions
SELECT subject_id,
marks,
AVG(marks) OVER
(
PARTITION BY subject_id
) AS average_marks
FROM Mark;

-- 37. Display previous exam marks for each student using LAG()
SELECT student_id,
exam_date,
marks,
LAG(marks) OVER
(
PARTITION BY student_id
ORDER BY exam_date
) AS previous_marks
FROM Mark;

-- 38. Display next exam marks for each student using LEAD()
SELECT student_id,
exam_date,
marks,
LEAD(marks) OVER
(
PARTITION BY student_id
ORDER BY exam_date
) AS next_marks
FROM Mark;

-- 39. Find the highest marks within each subject using MAX() OVER()
SELECT student_id,
subject_id,
marks,
MAX(marks) OVER
(
PARTITION BY subject_id
) AS highest_marks
FROM Mark;

-- 40. Display cumulative average marks ordered by exam date
SELECT exam_date,
marks,
AVG(marks) OVER
(
ORDER BY exam_date
ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
) AS cumulative_average
FROM Mark;

-- 41. Find the first student admitted in each department
SELECT *
FROM
(
SELECT s.student_name,
d.department_name,
s.admission_year,
ROW_NUMBER() OVER
(
PARTITION BY d.department_name
ORDER BY s.admission_year
) AS rn
FROM Student s
JOIN Department d
ON s.department_id = d.department_id
) t
WHERE rn = 1;

-- 42. Display the latest hired staff member in each department
SELECT *
FROM
(
SELECT st.staff_name,
d.department_name,
st.hire_date,
ROW_NUMBER() OVER
(
PARTITION BY d.department_name
ORDER BY st.hire_date DESC
) AS rn
FROM Staff st
JOIN Department d
ON st.department_id = d.department_id
) t
WHERE rn = 1;

-- 43. Divide students into 4 CGPA quartiles using NTILE()
SELECT student_name,
cgpa,
NTILE(4) OVER (ORDER BY cgpa DESC) AS quartile
FROM Student;

-- 44. Find percentage rank of students based on CGPA
SELECT student_name,
cgpa,
PERCENT_RANK() OVER (ORDER BY cgpa DESC) AS percentage_rank
FROM Student;

-- 45. Display cumulative distribution of salaries
SELECT staff_name,
salary,
CUME_DIST() OVER (ORDER BY salary DESC) AS cumulative_distribution
FROM Staff;

-- 46. Find subjects where a student's marks are above the subject average
SELECT s.student_name,
sub.subject_name,
m.marks
FROM Mark m
JOIN Student s
ON m.student_id = s.student_id
JOIN Subject sub
ON m.subject_id = sub.subject_id
WHERE m.marks >
(
SELECT AVG(m2.marks)
FROM Mark m2
WHERE m2.subject_id = m.subject_id
);

-- 47. Find departments whose average staff salary is higher than overall average salary
SELECT d.department_name,
AVG(st.salary) AS average_salary
FROM Department d
JOIN Staff st
ON d.department_id = st.department_id
GROUP BY d.department_name
HAVING AVG(st.salary) >
(
SELECT AVG(salary)
FROM Staff
);

-- 48. Display students who scored above department average marks
SELECT s.student_name,
m.marks
FROM Student s
JOIN Mark m
ON s.student_id = m.student_id
WHERE m.marks >
(
SELECT AVG(m2.marks)
FROM Mark m2
JOIN Student s2
ON m2.student_id = s2.student_id
WHERE s2.department_id = s.department_id
);

-- 49. Find the 3rd highest mark using DENSE_RANK()
SELECT *
FROM
(
SELECT student_id,
subject_id,
marks,
DENSE_RANK() OVER (ORDER BY marks DESC) AS dense_rank_number
FROM Mark
) t
WHERE dense_rank_number = 3;

-- 50. Generate a report showing student name, department, subject, exam type, marks, department average, and overall rank
SELECT s.student_name,
d.department_name,
sub.subject_name,
m.exam_type,
m.marks,
AVG(m.marks) OVER
(
PARTITION BY d.department_name
) AS department_average,
RANK() OVER
(
ORDER BY m.marks DESC
) AS overall_rank
FROM Mark m
JOIN Student s
ON m.student_id = s.student_id
JOIN Department d
ON s.department_id = d.department_id
JOIN Subject sub
ON m.subject_id = sub.subject_id;
