# Full Lifecycle E-Commerce Database Project

This project was completed as part of my Master's of Science in IT degree, Databases course, showcasing the complete design and administration lifecycle for a new e-commerce 
database. As the sole database architect, my role was to take a business concept and build it from the ground up, starting with foundational theory, moving to conceptual 
modeling (ERD), defining reliability (ACID), and implementing practical, high-performance SQL solutions (Indexes and Views).

## Table of Contents for Repository Artifacts
| File Number | Title | Description |
| :---------: | ----- | ----------- |
| 1 | [E-Commerce_ERD.png](E-Commerce_ERD.png) | The final Entity-Relationship Diagram for the database. |
| 2 | README.md | This current page with all relevant information about the project. |

---

## Table of Contents for README
| Section Title | Description |
| ------------- | ----------- |
| [Description](#description) | Describes the final product's purpose, software, format, and included visuals. |
| [Process](#process) | Describes the end-to-end design and implementation process. |
| [Data](#data) | Describes the data model, including key entities and their relationships. |
| [Assumptions](#assumptions) | Describes the core business requirements that guided the design. |
| [Key Design Outcomes](#key-design-outcomes) | Lists the practical SQL implementations for performance and security. |
| [Strategic Recommendations](#strategic-recommendations) | Recommended high-level strategies based on the analysis. |
| [Technologies Used](#technologies-used) | Lists the technologies and concepts applied in this project. |


### Description:
* **Software:** SQL, ERD Modeling Tool
* **Deliverables:** This project includes a complete conceptual data model, a physical Entity-Relationship Diagram (ERD), and a series of SQL (DDL) scripts for optimization
and security.
* **Analytical Formats:**
    * Conceptual & Logical Database Design
    * ACID Transaction Management Strategy
    * Cloud Deployment Strategy (DBaaS vs. Self-Managed)
    * SQL DDL for Performance (Indexes) and Security (Views)

### Process:
This project followed a 5-step lifecycle, moving from high-level business theory to practical, production-ready code.

**Step 1: Foundational Analysis**
The stakeholder, moving from in-person sales to e-commerce, asked the business question: For a new e-commerce app, why use a DBMS instead of a simple file system? The 
analysis concluded that file systems were unsuitable due to data redundancy, difficulty in accessing data, and a critical failure to manage concurrent transactions (e.g., 
two customers buying the last item in stock).

**Step 2: The Blueprint**
The next step was to design the architectural blueprint. This involved identifying all core business entities 
(like `customer`, `product`, `order`) and mapping their relationships into a physical Entity-Relationship Diagram (ERD) using Crow's Foot notation.

**Step 3: Ensuring Real-World Reliability (ACID Transactions)**
A design must be able to handle real-world transactions safely. This step involved defining the strategy for ACID (Atomicity, Consistency, Isolation, Durability) 
properties. For a customer purchase (which involves updating inventory, creating an order, and processing a payment), an ACID-compliant transaction 
(`BEGIN TRANSACTION`, `COMMIT`, `ROLLBACK`) is required to guarantee "all or nothing" execution. This prevents data corruption, such as a payment failing while an order is 
still created.

**Step 4: Strategic Deployment**
The analysis compared a self-managed (on-premise) solution with a managed cloud solution (DBaaS - Database as a Service). The conclusion was that a DBaaS (like Google Cloud 
SQL or Amazon RDS) is the clear winner for a new e-commerce app due to its rapid scalability, lower upfront cost, and reduced management overhead.

**Step 5: Practical Implementation & Optimization (SQL)**
The final step was to write the SQL (DDL) to build and optimize the database for a high-traffic environment. This focused on two key areas: creating performance-enhancing 
**Indexes** to speed up common queries (like customer logins) and creating **Views** to simplify complex reporting and secure sensitive data.

### Data
The database schema was designed to support all core functions of an e-commerce platform. The final design consists of 8 core entities:

* **`customer`**: Stores user account information (name, email, etc.).
* **`address`**: Stores multiple shipping addresses per customer.
* **`product`**: The catalog of items for sale, linked to categories and suppliers.
* **`category`**: Organizes products (e.g., "Electronics," "Apparel").
* **`supplier`**: Tracks vendors who provide the products.
* **`order`**: A record of a single purchase transaction, linked to a customer and shipping address.
* **`order_products`**: A linking table to resolve the many-to-many relationship between orders and products.
* **`review`**: Stores customer feedback and ratings for products.

## Assumptions:
The entire design was guided by a set of core business requirements, which formed the project's assumptions:
* **Data Integrity is paramount:** The system must prevent data redundancy and inconsistency (e.g., a customer's old address should not persist in a separate file).
* **Concurrency is a given:** The system must be able to handle multiple users at once without failure (e.g., managing simultaneous purchases of a single item).
* **Scalability is non-negotiable:** The system must be able to grow from 100 users to 1,000,000 users without a complete redesign.
* **Performance is a feature:** Users expect key pages (like "Login" and "Order History") to load instantly.
* **Security is required:** Sensitive data (like password hashes) must be restricted, while non-sensitive data (like sales reports) must be made easily accessible to other
teams.

### Key Design Outcomes:
The primary technical outcomes of this project were the SQL scripts designed to optimize and secure the database, ensuring it could meet the project's assumptions.

**1. Performance Optimization with Indexes**
* **Use Case:** Customer Login (to prevent a full-table scan on a table with millions of users).
* **SQL Implementation:**
    ```sql
    CREATE INDEX idx_customer_email
    ON customers(email);
    ```
* **Use Case:** User's Order History (to instantly load a customer's "My Orders" page).
* **SQL Implementation:**
    ```sql
    CREATE INDEX idx_order_customer
    ON orders(customer_id);
    ```

**2. Security & Simplification with Views**
* **Use Case:** Simplifying Sales Reporting (to give the marketing team a simple report of total sales per product without forcing them to write a complex JOIN).
* **SQL Implementation:**
    ```sql
    CREATE VIEW v_product_sales AS
    SELECT
        p.product_name AS product,
        pc.category_name AS category,
        SUM(od.quantity) AS total_quantity_sold
    FROM
        order_details od
        JOIN products p ON od.product_id = p.product_id
        JOIN product_categories pc ON p.category_id = pc.category_id
    GROUP BY
        product,
        category;
    ```

### Strategic Recommendations:
The analysis from the coursework resulted in three high-level strategic recommendations for launching this new e-commerce application.

* **Recommendation 1: Adopt a DBMS.** A Database Management System (DBMS) is the only viable choice. Its ability to manage concurrency, ensure data consistency, and provide
a single source of truth is essential for any scalable e-commerce platform.
* **Recommendation 2: Enforce ACID-Compliant Transactions.** All multi-step operations that involve money or inventory (like a customer purchase) *must* be wrapped in a
transaction. This guarantees "all or nothing" atomicity and is the only way to ensure data integrity.
* **Recommendation 3: Deploy on a Managed (DBaaS) Platform.** A managed cloud database (like Google Cloud SQL or Amazon RDS) is the clear winner for a new application. It
allows the business to scale on demand and focus on building its application, not managing servers.

### Technologies Used:
* Conceptual Modeling & E-R Diagrams
* Relational Database Design
* ACID Transaction Management
* Database Deployment Strategy (DBaaS)
* SQL (Data Definition Language)
* Performance Tuning (Indexes)
* Database Security (Views)
