# NetLearnPro
-- Создание базы данных NetLearnPro
CREATE DATABASE IF NOT EXISTS NetLearnPro;

-- Использование созданной базы данных
USE NetLearnPro;

-- Таблица для хранения информации о курсах
CREATE TABLE IF NOT EXISTS Courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,
    course_name VARCHAR(255) NOT NULL,
    course_description TEXT,
    instructor_name VARCHAR(255) NOT NULL
);

-- Таблица для хранения информации о студентах
CREATE TABLE IF NOT EXISTS Students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    student_name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    registration_date DATE NOT NULL
);

-- Таблица для хранения информации о занятиях
CREATE TABLE IF NOT EXISTS Lessons (
    lesson_id INT AUTO_INCREMENT PRIMARY KEY,
    lesson_name VARCHAR(255) NOT NULL,
    course_id INT,
    lesson_date DATE,
    FOREIGN KEY (course_id) REFERENCES Courses(course_id)
);

-- Таблица для отслеживания участия студентов в занятиях
CREATE TABLE IF NOT EXISTS StudentAttendance (
    attendance_id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    lesson_id INT,
    attendance_status VARCHAR(50) NOT NULL,
    FOREIGN KEY (student_id) REFERENCES Students(student_id),
    FOREIGN KEY (lesson_id) REFERENCES Lessons(lesson_id)
);

-- Таблица для хранения информации о заданиях
CREATE TABLE IF NOT EXISTS Assignments (
    assignment_id INT AUTO_INCREMENT PRIMARY KEY,
    assignment_name VARCHAR(255) NOT NULL,
    course_id INT,
    due_date DATE,
    FOREIGN KEY (course_id) REFERENCES Courses(course_id)
);

-- Таблица для отслеживания представления студентами заданий
CREATE TABLE IF NOT EXISTS StudentAssignments (
    submission_id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    assignment_id INT,
    submission_date DATE,
    grade FLOAT,
    FOREIGN KEY (student_id) REFERENCES Students(student_id),
    FOREIGN KEY (assignment_id) REFERENCES Assignments(assignment_id)
);

