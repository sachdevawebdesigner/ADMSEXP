DROP TABLE IF EXISTS StudentEnrollments;

CREATE TABLE StudentEnrollments (
    enrollment_id INT AUTO_INCREMENT PRIMARY KEY,
    student_name VARCHAR(100) NOT NULL,
    course_id VARCHAR(10) NOT NULL,
    enrollment_date DATE NOT NULL,
    CONSTRAINT unique_student_course UNIQUE (student_name, course_id)
);

INSERT INTO StudentEnrollments (student_name, course_id, enrollment_date)
VALUES
('Ashish', 'CSE101', '2024-07-01'),
('Smaran', 'CSE102', '2024-07-01'),
('Vaibhav', 'CSE103', '2024-07-01');

SELECT * FROM StudentEnrollments;

START TRANSACTION;
INSERT INTO StudentEnrollments (student_name, course_id, enrollment_date)
VALUES ('Rohan', 'CSE104', '2024-07-01');

START TRANSACTION;
INSERT INTO StudentEnrollments (student_name, course_id, enrollment_date)
VALUES ('Rohan', 'CSE105', '2024-07-01');

COMMIT;

START TRANSACTION;
SELECT * FROM StudentEnrollments
WHERE student_name = 'Ashish' AND course_id = 'CSE101'
FOR UPDATE;

START TRANSACTION;
UPDATE StudentEnrollments
SET enrollment_date = '2024-08-01'
WHERE student_name = 'Ashish' AND course_id = 'CSE101';

COMMIT;
COMMIT;

START TRANSACTION;
SELECT * FROM StudentEnrollments
WHERE student_name = 'Smaran' AND course_id = 'CSE102'
FOR UPDATE;
UPDATE StudentEnrollments
SET enrollment_date = '2024-09-01'
WHERE student_name = 'Smaran' AND course_id = 'CSE102';
COMMIT;

START TRANSACTION;
SELECT * FROM StudentEnrollments
WHERE student_name = 'Smaran' AND course_id = 'CSE102'
FOR UPDATE;
UPDATE StudentEnrollments
SET enrollment_date = '2024-10-01'
WHERE student_name = 'Smaran' AND course_id = 'CSE102';
COMMIT;

SELECT * FROM StudentEnrollments;
