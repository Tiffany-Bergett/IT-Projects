# University Database Lifecycle: Design, Implementation, & Optimization

This project simulates the complete lifecycle of a database, from initial design to production-ready optimization. As the project's Database Administrator (DBA), I took a single, denormalized table and engineered a secure, efficient, and reliable 3NF database. This repository contains all the SQL scripts and analysis documents demonstrating the multi-stage process.

## Table of Contents for Repository Artifacts

| File Number | Title | Description |
| :---: | ----- | ----------- |
| 1 | [Normalization_Analysis.md](URL HERE) | A complete write-up of the initial database design, anomaly analysis, and the 3NF normalization process. |
| 2 | [DDL_Implementation.sql](URL HERE) | The DDL script used to `CREATE` the normalized 3NF schema, including all tables, primary keys, and constraints. |
| 3 | [DML_Queries.sql](URL HERE) | A collection of DML scripts used to `INSERT` sample data and `SELECT`, `UPDATE`, and `DELETE` records. |
| 4 | [Optimization_Scripts.sql](URL HERE) | The DDL script used to create performance-enhancing `INDEX`es and secure reporting `VIEW`s. |
| 5 | [Security_and_Recovery_Plan.md](URL HERE) | An analysis of the Role-Based Access Control (RBAC) strategy and the full backup/recovery plan. |

---

## Table of Contents for README

| Section Title | Description |
| ------------- | ----------- |
| [Project Overview](#project-overview) | The project's purpose, software, and final deliverable. |
| [The Database Lifecycle](#the-database-lifecycle) | A step-by-step description of the four-phase project process. |
| [Final Schema](#final-schema) | A description of the final, normalized database tables and fields. |
| [Key Optimizations](#key-optimizations) | A summary of the indexes and views created to enhance performance and security. |
| [Security & Recovery](#security--recovery-plan) | A high-level overview of the data protection and recovery strategy. |
| [Notes](#notes) | Project context. |

### Project Overview
* **Software:** MySQL
* **Format:** This project is a collection of `.sql` scripts and analysis write-ups. It demonstrates the *process* of database engineering, from logical design to physical
implementation and performance tuning.

### The Database Lifecycle
This project was executed in four distinct phases, simulating the real-world responsibilities of a DBA.

1.  **Phase 1: Normalization (Design):** The project began with a single, flawed, denormalized table (`CourseEnrollment`). I analyzed its insertion, deletion, and update
anomalies, identified all functional dependencies, and then normalized the schema to the Third Normal Form (3NF).
2.  **Phase 2: Implementation (Build):** I wrote `DDL` (Data Definition Language) scripts to `CREATE` the new 3NF schema, consisting of `Student`, `Course`, and
 `CourseEnrollment` tables. This included implementing primary keys, foreign keys, and `NOT NULL` constraints. I then used `DML` (Data Manipulation Language) to populate the
tables and run realistic queries using `JOINs`.
3.  **Phase 3: Optimization (Tune):** With the database built, I shifted focus to performance. I created `INDEXes` on frequently queried columns (like user emails and IDs) to
 accelerate lookups. I also designed and implemented `VIEWs` to simplify complex reporting queries and secure sensitive data.
4.  **Phase 4: Management (Secure):** Finally, I designed a robust Role-Based Access Control (RBAC) strategy using `GRANT` and `REVOKE` to manage permissions. I also outlined
a full disaster recovery plan, detailing the backup (Full, Differential, Log) and recovery (Point-in-Time) procedures.

### Final Schema
The final normalized database consists of three tables:
* **`Student`**: Stores all student-specific data.
    * `StudentID`: Primary Key
    * `StudentName`
* **`Course`**: Stores all course-specific data.
    * `CourseID`: Primary Key
    * `CourseName`
    * `CreditHours`
* **`CourseEnrollment`**: A junction table that links students and courses.
    * `CourseID`: Composite Primary Key, Foreign Key
    * `StudentID`: Composite Primary Key, Foreign Key
    * `Grade`

### Key Optimizations
To improve the performance and usability of the database, the following objects were created:
* **`idx_customer_email` (Index):** Placed on the `Customer.Email` column. This is critical for accelerating login authentication, as it allows the database to instantly find a user's record without a full table scan.
* **`v_product_sales` (View):** A non-updatable view that joins multiple tables to create a simple, pre-built sales report. This simplifies complex queries for the marketing team.
* **`v_admin_users` (View):** An updatable view that securely exposes only the non-sensitive data for users with an 'admin' role. This allows internal tools to manage admins without having access to sensitive fields like password hashes.

### Security & Recovery Plan

* **Security:** A Role-Based Access Control (RBAC) plan was designed. This involves creating roles (e.g., `Medical_Staff`, `Admin_Staff`) and using `GRANT` statements to assign the minimum necessary permissions (e.g., `SELECT`, `INSERT`) to those roles, adhering to the principle of least privilege.
* **Recovery:** A full disaster recovery strategy was outlined. It uses a combination of weekly **Full Backups**, daily **Differential Backups**, and frequent **Transaction Log Backups**. This strategy ensures the organization can perform a point-in-time recovery, minimizing data loss in the event of a catastrophic failure.

### Notes
This project was completed as part of the Master of Science in Information Technology program, demonstrating a comprehensive understanding of database design, implementation, and administration.
