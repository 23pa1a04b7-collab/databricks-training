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


# COLLEGE MANAGEMENT SYSTEM SQL PRACTICE QUESTIONS & QUERIES

## 1. List all students along with their department names.

```sql
SELECT s.student_name, d.department_name
FROM Student s
LEFT JOIN Department d
ON s.department_id = d.department_id;
```

---

## 2. Display all staff members and their department names, including staff without departments.

```sql
SELECT st.staff_name, d.department_name
FROM Staff st
LEFT JOIN Department d
ON st.department_id = d.department_id;
```

---

## 3. Find all departments that currently have no students assigned.

```sql
SELECT d.department_name
FROM Department d
LEFT JOIN Student s
ON d.department_id = s.department_id
WHERE s.student_id IS NULL;
```

---

## 4. Show students who do not have any marks recorded.

```sql
SELECT s.student_name
FROM Student s
LEFT JOIN Mark m
ON s.student_id = m.student_id
WHERE m.student_id IS NULL;
```

---

## 5. Display subjects that are not assigned to any staff member.

```sql
SELECT subject_name
FROM Subject
WHERE staff_id IS NULL;
```

---

## 6. Find the average CGPA department-wise.

```sql
SELECT d.department_name, AVG(s.cgpa) AS average_cgpa
FROM Department d
LEFT JOIN Student s
ON d.department_id = s.department_id
GROUP BY d.department_name;
```

---

## 7. Display departments where the average CGPA is greater than 8.0.

```sql
SELECT d.department_name, AVG(s.cgpa) AS average_cgpa
FROM Department d
JOIN Student s
ON d.department_id = s.department_id
GROUP BY d.department_name
HAVING AVG(s.cgpa) > 8.0;
```

---

## 8. Find the total number of students in each department.

```sql
SELECT d.department_name, COUNT(s.student_id) AS total_students
FROM Department d
LEFT JOIN Student s
ON d.department_id = s.department_id
GROUP BY d.department_name;
```

---

## 9. Display the highest and lowest marks scored in each subject.

```sql
SELECT sub.subject_name,
MAX(m.marks) AS highest_marks,
MIN(m.marks) AS lowest_marks
FROM Subject sub
JOIN Mark m
ON sub.subject_id = m.subject_id
GROUP BY sub.subject_name;
```

---

## 10. Find students who scored more than 90 in any exam.

```sql
SELECT DISTINCT s.student_name, m.marks
FROM Student s
JOIN Mark m
ON s.student_id = m.student_id
WHERE m.marks > 90;
```

---

## 11. Display the names of students who belong to the Computer Science department.

```sql
SELECT s.student_name
FROM Student s
JOIN Department d
ON s.department_id = d.department_id
WHERE d.department_name = 'Computer Science';
```

---

## 12. Find the number of subjects handled by each staff member.

```sql
SELECT st.staff_name, COUNT(sub.subject_id) AS total_subjects
FROM Staff st
LEFT JOIN Subject sub
ON st.staff_id = sub.staff_id
GROUP BY st.staff_name;
```

---

## 13. Display students along with the total marks they obtained across all subjects.

```sql
SELECT s.student_name, SUM(m.marks) AS total_marks
FROM Student s
LEFT JOIN Mark m
ON s.student_id = m.student_id
GROUP BY s.student_name;
```

---

## 14. Find departments with more than 2 staff members.

```sql
SELECT d.department_name, COUNT(st.staff_id) AS total_staff
FROM Department d
JOIN Staff st
ON d.department_id = st.department_id
GROUP BY d.department_name
HAVING COUNT(st.staff_id) > 2;
```

---

## 15. Display students whose CGPA is above the average CGPA.

```sql
SELECT student_name, cgpa
FROM Student
WHERE cgpa > (
    SELECT AVG(cgpa)
    FROM Student
);
```


















JOIN Subject sub
ON m.subject_id = sub.subject_id;
