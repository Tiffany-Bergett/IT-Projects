# University Database Design & Implementation

This project focuses on the foundational steps of database design and implementation. Starting with a single, denormalized table for a university course enrollment system, I performed a full normalization analysis to design a robust 3NF schema and then wrote the SQL scripts to build and populate the database. This repository contains the analysis and the SQL code.

## Table of Contents for Repository Artifacts

| File Number | Title                                   | Description                                                                                          |
| :---------: | --------------------------------------- | ---------------------------------------------------------------------------------------------------- |
|      1      | [Normalization_Analysis.md](URL HERE) | A complete write-up of the initial database design, anomaly analysis, and the 3NF normalization process. |
|      2      | [DDL_Implementation.sql](URL HERE)      | The DDL script used to `CREATE` the normalized 3NF schema using standard SQL.                        |
|      3      | [DML_Queries.sql](URL HERE)             | A collection of DML scripts used to `INSERT` sample data and `SELECT`, `UPDATE`, and `DELETE` records. |

---

## Table of Contents for README

| Section Title                        | Description                                                                      |
| ------------------------------------ | -------------------------------------------------------------------------------- |
| [Project Overview](#project-overview) | The project's purpose, software used for testing, and final deliverable format.  |
| [The Database Lifecycle](#the-database-lifecycle) | A step-by-step description of the two-phase project process.                     |
| [Final Schema](#final-schema)        | A description of the final, normalized database tables and fields.               |
| [Notes](#notes)                      | Project context and software notes.                                              |

### Project Overview
* **Software Used for Testing:** MySQL (via MySQL Workbench)
* **SQL Dialect:** Standard SQL (compatible with most RDBMS like MySQL, SQLite, PostgreSQL)
* **Format:** This project includes an analysis write-up (`.md`) and SQL scripts (`.sql`). It demonstrates the core process of database design (normalization) and implementation (DDL/DML).

### The Database Lifecycle
This project was executed in two distinct phases:

1.  **Phase 1: Normalization (Design):** The project began with a single, flawed, denormalized table (`CourseEnrollment`). I analyzed its insertion, deletion, and update anomalies, identified all functional dependencies, and then normalized the schema to the Third Normal Form (3NF).
2.  **Phase 2: Implementation (Build):** I wrote `DDL` (Data Definition Language) scripts to `CREATE` the new 3NF schema, consisting of `student`, `course`, and `enrollment` tables. This included implementing primary keys, foreign keys, and `NOT NULL` constraints. I then used `DML` (Data Manipulation Language) to populate the tables and run realistic queries using `JOIN`s, aggregate functions, `UPDATE`, and `DELETE` statements.

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

### Notes
* This project was completed as part of the Master of Science in Information Technology program, demonstrating core skills in database normalization and SQL implementation.
* The SQL code adheres to standard practices and was primarily tested using MySQL Workbench, though parts were conceptualized using SQLite principles during initial design phases.
