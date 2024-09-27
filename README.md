-1-
SELECT AVG(grade) AS average_grade
FROM Enrollments;

-2-
SELECT s.name AS student_name, c.course_name
FROM Students s
JOIN Enrollments e ON s.student_id = e.student_id
JOIN Courses c ON e.course_id = c.course_id;

-3-
SELECT grade_level, COUNT(student_id) AS student_count
FROM Students
GROUP BY grade_level;

-4-
SELECT c.course_name, MAX(e.grade) AS max_grade
FROM Courses c
JOIN Enrollments e ON c.course_id = e.course_id
GROUP BY c.course_name;

-5-
SELECT AVG(e.grade) AS average_grade
FROM Enrollments e
JOIN Students s ON e.student_id = s.student_id
WHERE s.grade_level = 3;

-6-
SELECT s.name AS student_name, c.course_name, c.credits
FROM Students s
JOIN Enrollments e ON s.student_id = e.student_id
JOIN Courses c ON e.course_id = c.course_id;

-7-
SELECT c.course_name, AVG(e.grade) AS average_grade
FROM Courses c
JOIN Enrollments e ON c.course_id = e.course_id
GROUP BY c.course_name
HAVING AVG(e.grade) > 3.0;

-8-
SELECT DISTINCT s.name AS student_name
FROM Students s
WHERE s.student_id NOT IN (
    SELECT e.student_id
    FROM Enrollments e
    WHERE e.grade = 4.0
);



-9-
WITH student_avg AS (
    SELECT student_id, AVG(grade) AS avg_grade
    FROM Enrollments
    GROUP BY student_id
),
overall_avg AS (
    SELECT AVG(grade) AS overall_average
    FROM Enrollments
)
SELECT s.name
FROM Students s
JOIN student_avg sa ON s.student_id = sa.student_id
CROSS JOIN overall_avg oa
WHERE sa.avg_grade > oa.overall_average;



-10-
SELECT s.name AS student_name, COUNT(e.course_id) AS total_courses, AVG(e.grade) AS average_grade
FROM Students s
JOIN Enrollments e ON s.student_id = e.student_id
GROUP BY s.name;
