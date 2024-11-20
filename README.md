
CREATE TABLE Students (
    student_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    date_of_birth DATE,
    email VARCHAR(100)
);

CREATE TABLE Instructors (
    instructor_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    email VARCHAR(100)
);

CREATE TABLE Courses (
    course_id INT PRIMARY KEY AUTO_INCREMENT,
    course_name VARCHAR(100),
    course_description TEXT,
    instructor_id INT,
    FOREIGN KEY (instructor_id) REFERENCES Instructors(instructor_id)
);

CREATE TABLE Enrollments (
    enrollment_id INT PRIMARY KEY AUTO_INCREMENT,
    student_id INT,
    course_id INT,
    grade CHAR(1),
    FOREIGN KEY (course_id) REFERENCES Courses(course_id)
);
-- Inserting Data into Students
INSERT INTO Students (first_name, last_name, date_of_birth, email) VALUES
('John', 'Doe', '2000-05-15', 'john.doe@example.com'),
('Jane', 'Smith', '1999-07-22', 'jane.smith@example.com'),
('Sam', 'Wilson', '2001-09-10', 'sam.wilson@example.com');

-- Inserting Data into Instructors
INSERT INTO Instructors (first_name, last_name, email) VALUES
('Emma', 'Brown', 'emma.brown@example.com'),
('Michael', 'Johnson', 'michael.johnson@example.com');

-- Inserting Data into Courses
INSERT INTO Courses (course_name, course_description, instructor_id) VALUES
('Math 101', 'Introduction to Algebra', 1),
('History 202', 'World History Overview', 2),
('Physics 301', 'Basics of Mechanics', 1);

-- Inserting Data into Enrollments
INSERT INTO Enrollments (student_id, course_id, grade) VALUES
(1, 1, 'A'),
(2, 1, 'B'),
(3, 2, 'A'),
(1, 3, 'C'),
(2, 3, 'B');
 
 -- List All Students and Their Grades
 SELECT 
    s.first_name, 
    s.last_name, 
    c.course_name, 
    e.grade
FROM 
    Enrollments e
JOIN 
    Students s ON e.student_id = s.student_id
JOIN 
    Courses c ON e.course_id = c.course_id;
    --  Calculate Average Grade for a Course
    SELECT 
    c.course_name, 
    AVG(CASE 
        WHEN e.grade = 'A' THEN 4
        WHEN e.grade = 'B' THEN 3
        WHEN e.grade = 'C' THEN 2
        WHEN e.grade = 'D' THEN 1
        ELSE 0 
    END) AS average_grade
FROM 
    Enrollments e
JOIN 
    Courses c ON e.course_id = c.course_id
WHERE 
    c.course_name = 'Math 101';


