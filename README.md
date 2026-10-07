- Week 1 Database Systems Assignment
-- Project: School Management Database
-- Purpose: Store students, courses, and enrollments.

-- 1. Create the database
CREATE DATABASE IF NOT EXISTS school_management;

-- 2. Select the database
USE school_management;

-- 3. Create the students table
CREATE TABLE IF NOT EXISTS students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    age INT,
    email VARCHAR(100) UNIQUE
);

-- 4. Create the courses table
CREATE TABLE IF NOT EXISTS courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    course_code VARCHAR(20) UNIQUE
);

-- 5. Create the enrollments table
CREATE TABLE IF NOT EXISTS enrollments (
    enrollment_id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT NOT NULL,
    course_id INT NOT NULL,
    enrollment_date DATE,
    FOREIGN KEY (student_id)
        REFERENCES students(student_id),
    FOREIGN KEY (course_id)
        REFERENCES courses(course_id)
);

-- 6. Insert sample students
INSERT INTO students (first_name, last_name, age, email)
VALUES
('John', 'James', 20, 'john@example.com'),
('Mary', 'Peter', 19, 'mary@example.com'),
('David', 'Paul', 21, 'david@example.com');

-- 7. Insert sample courses
INSERT INTO courses (course_name, course_code)
VALUES
('Database Systems', 'DBS101'),
('Web Development', 'WEB101'),
('Computer Programming', 'CP101');

-- 8. Enroll students in courses
INSERT INTO enrollments (student_id, course_id, enrollment_date)
VALUES
(1, 1, '2026-10-07'),
(2, 2, '2026-10-07'),
(3, 3, '2026-10-07');

-- 9. Display all students
SELECT * FROM students;

-- 10. Display all courses
SELECT * FROM courses;

-- 11. Display student enrollments
SELECT
    students.first_name,
    students.last_name,
    courses.course_name,
    enrollments.enrollment_date
FROM enrollments
JOIN students
    ON enrollments.student_id = students.student_id
JOIN courses
    ON enrollments.course_id = courses.course_id;
