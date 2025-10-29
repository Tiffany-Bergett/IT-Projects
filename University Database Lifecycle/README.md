# University Database Lifecycle: Design, Implementation, & Optimization

This project simulates the complete lifecycle of a university course enrollment database, from initial design to production-ready optimization. As the project's Database Administrator (DBA), I took a single, denormalized table and engineered a secure, efficient, and reliable 3NF database using standard SQL. This repository contains all the SQL scripts and analysis documents demonstrating the multi-stage process.

## Table of Contents for Repository Artifacts

| File Number | Title                                        | Description                                                                                          |
| :---------: | -------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
|      1      | [Normalization_Analysis.md](URL HERE)        | A complete write-up of the initial database design, anomaly analysis, and the 3NF normalization process. |
|      2      | [DDL_Implementation.sql](URL HERE)           | The DDL script used to `CREATE` the normalized 3NF schema using standard SQL.                        |
|      3      | [DML_Queries.sql](URL HERE)                  | A collection of DML scripts used to `INSERT` sample data and `SELECT`, `UPDATE`, and `DELETE` records. |
|      4      | [Optimization_Scripts.sql](URL HERE)         | The DDL script used to create performance-enhancing `INDEX`es and reporting `VIEW`s for the university schema. |
|      5      | [Security_and_Recovery_Plan.md](URL HERE) | An analysis of a Role-Based Access Control (RBAC) strategy and a full backup/recovery plan.        |

---

## Table of Contents for README

| Section Title                        | Description                                                                      |
| ------------------------------------ | -------------------------------------------------------------------------------- |
| [Project Overview](#project-overview) | The project's purpose, software used for testing, and final deliverable format.  |
| [The Database Lifecycle](#the-database-lifecycle) | A step-by-step description of the four-phase project process.                    |
| [Final Schema](#final-schema)        | A description of the final, normalized database tables and fields.               |
| [Key Optimizations](#key-optimizations)  | A summary of the indexes and views created to enhance performance and usability. |
| [Security & Recovery](#security--recovery-plan) | A high-level overview of the data protection and recovery strategy discussed.    |
| [Notes](#notes)                      | Project context and software notes.                                              |

### Project Overview
* **Software Used for Testing:** MySQL (via MySQL Workbench)
* **SQL Dialect:** Standard SQL (compatible with most RDBMS like MySQL, SQLite, PostgreSQL)
* **Format:** This project is a collection of `.sql` scripts and analysis write-ups. It demonstrates the *process* of database engineering, from logical design to physical implementation and performance tuning.

### The Database Lifecycle
This project was executed in four distinct phases, simulating the real-world responsibilities of a DBA.

1.  **Phase 1: Normalization (Design):** The project began with a single, flawed, denormalized table (`CourseEnrollment`). I analyzed its insertion, deletion, and update anomalies, identified all functional dependencies, and then normalized the schema to the Third Normal Form (3NF).
2.  **Phase 2: Implementation (Build):** I wrote `DDL` (Data Definition Language) scripts to `CREATE` the new 3NF schema, consisting of `student`, `course`, and `enrollment` tables. This included implementing primary keys, foreign keys, and `NOT NULL` constraints. I then used `DML` (Data Manipulation Language) to populate the tables and run realistic queries using `JOIN`s, aggregate functions, and `GROUP BY`/`HAVING` clauses.
3.  **Phase 3: Optimization (Tune):** With the database built, I shifted focus to performance and usability. I created `INDEX`es on frequently queried columns (like student and course names) to accelerate lookups. I also designed and implemented `VIEW`s to simplify common reporting queries.
4.  **Phase 4: Management (Secure):** Finally, I analyzed a robust Role-Based Access Control (RBAC) strategy (using example roles like `Faculty_Staff` and `Classified_Staff`) and outlined a full disaster recovery plan, detailing the backup (Full, Differential, Log) and recovery (Point-in-Time) procedures necessary for a production system.

### Final Schema
The final normalized database consists of three tables:
* **`student`**: Stores all student-specific data.
    * `student_id`: Primary Key (VARCHAR)
    * `student_name`: VARCHAR, NOT NULL
* **`course`**: Stores all course-specific data.
    * `course_id`: Primary Key (VARCHAR)
    * `course_name`: VARCHAR, NOT NULL
    * `credit_hours`: INT
* **`enrollment`**: A junction table that links students and courses.
    * `student_id`: Composite Primary Key, Foreign Key (VARCHAR)
    * `course_id`: Composite Primary Key, Foreign Key (VARCHAR)
    * `grade`: CHAR(1)

### Key Optimizations
To improve the performance and usability of the university database, the following objects could be created:
* **`idx_student_name` (Index):** Placed on the `student.student_name` column. This accelerates lookups when searching for a student by name (e.g., finding Tiffany Bergett's grade).
* **`idx_course_name` (Index):** Placed on the `course.course_name` column. This speeds up queries filtering by course name (e.g., finding all enrollments in 'Databases').
* **`v_student_grades` (View):** A view joining `student`, `enrollment`, and `course` tables to provide a simple way to see all grades for all students across all courses, hiding the complexity of the underlying `JOIN`s.

### Security & Recovery Plan

* **Security:** A Role-Based Access Control (RBAC) plan was analyzed using example roles (`Administrator`, `Faculty_Staff`, `Classified_Staff`). This involves using `GRANT` statements to assign the minimum necessary permissions (e.g., `SELECT`, `INSERT`) to roles, adhering to the principle of least privilege.
* **Recovery:** A full disaster recovery strategy was outlined. It uses a combination of weekly **Full Backups**, daily **Differential Backups**, and frequent **Transaction Log Backups**. This strategy ensures the organization can perform a point-in-time recovery, minimizing data loss in the event of a catastrophic failure.

### Notes
* This project was completed as part of the Master of Science in Information Technology program, demonstrating a comprehensive understanding of database design, implementation, and administration.
* The SQL code adheres to standard practices and was primarily tested using MySQL Workbench, though parts were conceptualized using SQLite principles during initial design phases.
