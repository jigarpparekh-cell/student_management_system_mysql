# Student Management System — Database Design Mini Project

A GitHub-ready relational database mini project built with **MySQL 8.0+**. It manages students, departments, instructors, courses, semesters, enrollments, attendance, assessments, and marks.

## Project overview

Educational institutions need a consistent way to store student and academic information. This project models those records in a normalized relational database and demonstrates practical SQL operations and reporting queries.

### Main features

- Maintain departments, students, instructors, courses, and semesters.
- Enroll students in course offerings for a semester.
- Record attendance against a student's enrollment.
- Create assessments and store student marks.
- Generate student transcripts, course rosters, attendance summaries, and result reports.
- Enforce data integrity through primary keys, foreign keys, unique constraints, and check constraints.

## Technology

- Database: MySQL 8.0 or later
- SQL dialect: MySQL
- Diagram: Mermaid ER diagram
- Recommended client: MySQL Workbench, DBeaver, or MySQL command line

## Repository structure

```text
student-management-system/
├── README.md
├── LICENSE
├── .gitignore
├── docs/
│   ├── er-diagram.md
│   └── normalization.md
└── sql/
    ├── 01_create_database.sql
    ├── 02_schema.sql
    ├── 03_sample_data.sql
    ├── 04_views.sql
    └── 05_queries.sql
```

## Database design

The design separates independent entities and uses junction tables for many-to-many relationships.

- A department has many students, instructors, and courses.
- An instructor can teach many course offerings.
- A course can be offered in multiple semesters.
- Students register for offerings through `enrollments`.
- Attendance and assessment marks are recorded against an enrollment.
- Each assessment belongs to one course offering.

See [`docs/er-diagram.md`](docs/er-diagram.md) for the Mermaid ER diagram and [`docs/normalization.md`](docs/normalization.md) for the normalization explanation.

## Setup instructions

### 1. Install and start MySQL

Use MySQL Server 8.0+ and connect through MySQL Workbench or a terminal.

### 2. Run the SQL files in order

From the project root, execute:

```bash
mysql -u root -p < sql/01_create_database.sql
mysql -u root -p student_management_system < sql/02_schema.sql
mysql -u root -p student_management_system < sql/03_sample_data.sql
mysql -u root -p student_management_system < sql/04_views.sql
```

Then open `sql/05_queries.sql` in your SQL client and run the queries individually.

> The first script drops and recreates the project database. Do not run it against a database containing data you need to keep.

### 3. Verify the setup

```sql
USE student_management_system;
SHOW TABLES;
SELECT * FROM students;
SELECT * FROM vw_student_academic_summary;
```

## Example reports

The query collection includes:

1. Student list with department names.
2. Students enrolled in each semester.
3. Course roster with instructor details.
4. Attendance percentage per student and course.
5. Assessment-wise marks and percentages.
6. Student transcript / result summary.
7. Courses with the highest enrollment.
8. Students with attendance below 75%.
9. Department-wise student counts.
10. Students who have not enrolled in a semester.

## Data model notes

- `student_id`, `course_id`, etc. are surrogate primary keys.
- Student email and student number are unique.
- A student can enroll in a course offering only once.
- Attendance is stored as one row per enrollment per class date.
- Assessment marks are constrained to be between zero and the assessment's maximum marks.
- `assessment_results` uses a composite primary key to prevent duplicate marks for the same assessment and enrollment.

## Suggested GitHub upload

1. Create a new public repository named `student-management-system`.
2. Extract this project ZIP.
3. Upload the files while preserving the folder structure, or run:

```bash
git init
git add .
git commit -m "Add Student Management System database project"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/student-management-system.git
git push -u origin main
```

Replace `YOUR-USERNAME` with your GitHub username.

## Future enhancements

- Add role-based access for administrators, faculty, and students.
- Add fee payments and timetable management.
- Build a web application/API connected to this database.
- Add stored procedures for enrollment and grade calculation.
- Add automated tests and larger generated datasets.

## Author

Add your name, course, institution, and academic year here before submitting.

## License

This project is provided for educational use under the MIT License. See [`LICENSE`](LICENSE).
