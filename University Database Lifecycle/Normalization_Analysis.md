# Analysis and Normalization of the CourseEnrollment Schema
A well-designed relational database is critical for data integrity and efficiency. The relational model, which describes the world as a "collection of interrelated relations
(or tables)," serves as the foundation for modern database systems. The process of normalization provides a systematic method for organizing 
attributes within these tables to minimize data redundancy and avoid destructive anomalies. This analysis examines the initial `CourseEnrollment` schema, identifies its 
design flaws, and normalizes it to the Third Normal Form (3NF).

## Initial Schema
`CourseEnrollment (CourseID, CourseName, StudentID, StudentName, CreditHours, Grade)`

## a. First Normal Form (1NF) Identification
A relation is in First Normal Form (1NF) if all its attributes are atomic, meaning each cell contains only a single, indivisible value. The `CourseEnrollment` schema adheres 
to this rule. Each attribute (CourseID, StudentID, Grade, etc.) holds a single value per record. Therefore, the schema is in 1NF.

## b. Functional Dependencies
Functional dependencies define relationships where one set of attributes determines another. The dependencies in this schema are:
1.  `CourseID -> CourseName, CreditHours`
2.  `StudentID -> StudentName`
3.  `(CourseID, StudentID) -> Grade`
The composite key `(CourseID, StudentID)` is the only candidate for the primary key.

## c. Sample Records (Demonstrating Many-to-Many)
| CourseID | CourseName              | StudentID | StudentName    | CreditHours | Grade |
| :------- | :---------------------- | :-------- | :------------- | :---------- | :---- |
| CERM100  | Ceramics for Beginners  | B03042027 | Britany Miller | 4           | A     |
| CHID101  | Child Development Basics| B03042027 | Britany Miller | 4           | B     |
| MATS102  | Math Support 2          | C03172029 | Lilac Lloyde   | 1           | C     |
| MATS102  | Math Support 2          | J04182038 | Luna Berger    | 1           | D     |

## d. Design Anomalies
The schema suffers from modification anomalies due to data redundancy:
* **Insertion Anomaly:** Cannot add a new course until a student enrolls, because `StudentID` (part of the primary key) cannot be null.
* **Deletion Anomaly:** If the last student enrolled in a course is deleted, all information about the course itself is lost.

## e. Normalization to Third Normal Form (3NF)
### Normalization to 2NF
A relation is in Second Normal Form (2NF) if it is in 1NF and all non-key attributes are fully dependent on the primary key. The initial schema violates 2NF due to partial 
dependencies (`CourseName`, `CreditHours` depend only on `CourseID`; `StudentName` depends only on `StudentID`). Decomposition yields:
1.  **COURSE:** (`CourseID` (PK), `CourseName`, `CreditHours`)
2.  **STUDENT:** (`StudentID` (PK), `StudentName`)
3.  **ENROLLMENT:** (`CourseID` (FK), `StudentID` (FK), `Grade`) with PK `(CourseID, StudentID)`.

### Normalization to 3NF
A relation is in Third Normal Form (3NF) if it is in 2NF and has no transitive dependencies. Examining the three new tables reveals no transitive 
dependencies (where a non-key attribute determines another non-key attribute). All non-key attributes depend only on their respective primary keys.
Therefore, the decomposition to 2NF also achieves 3NF. This final design eliminates anomalies and reduces redundancy.
