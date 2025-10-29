# Database Security and Recovery Plan for a University

Ensuring the security and recoverability of student data is the highest priority for a database administrator (DBA). This The 
plan outlines the strategies for managing user access through roles and implementing a robust backup and recovery system.

## Part 1: Managing Roles and Secure Transactions

Security is enforced using Role-Based Access Control (RBAC), adhering to the principle of least privilege. Permissions are 
granted to roles, not individual users, simplifying management and reducing errors.

### Defined Roles:
* **Administrator:** Full database management privileges.
* **Certified_Staff:** Access required for student grading (e.g., `SELECT`, `UPDATE` on `CourseEnrollment`).
* **Administrative_Staff:** Access required for scheduling and inquiries (e.g., `SELECT`, `INSERT`, `UPDATE` on
`CourseEnrollment`).

### Example GRANT Statements:

```sql
-- Create the roles
CREATE ROLE Administrator;
CREATE ROLE Certified_Staff;
CREATE ROLE Administrative_Staff;

-- Grant permissions to Certified_Staff
GRANT SELECT, UPDATE ON CourseEnrollment TO Certified_Staff;

-- Grant permissions to Administrative Staff
GRANT SELECT, INSERT, UPDATE ON CourseEnrollment TO Administrative_Staff;

-- Administrator role would typically receive broader privileges via system grants
-- e.g., GRANT ALL PRIVILEGES ON DATABASE University_db TO Administrator; (Syntax varies by RDBMS)
