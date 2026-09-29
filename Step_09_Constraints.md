# 📘 STEP 9 — Constraints & Referential Integrity (60% → 68%)

---

## 🏆 SQL 0% → 100% Roadmap

```text
SQL
│
├── 0-5%     Database Fundamentals (STEP 1)
├── 5-10%    SQL Introduction & CRUD (STEP 2)
├── 10-15%   Data Types (STEP 3)
├── 15-25%   DDL Commands (STEP 4)
├── 25-35%   DML Commands (STEP 5)
├── 35-45%   DQL Commands / SELECT + WHERE (STEP 6)
├── 45-50%   Operators & Conditions (STEP 7)
├── 50-60%   Functions + GROUP BY + HAVING (STEP 8)
├── 60-68%   Constraints (STEP 9) 👈 (You are here)
├── 68-78%   JOINS (INNER, LEFT, RIGHT, FULL, CROSS, SELF) ⭐ (STEP 10)
├── 78-83%   Subqueries (STEP 11)
├── 83-88%   Views + Index + Sequence + Synonym (STEP 12)
├── 88-91%   DCL Commands (GRANT, REVOKE) (STEP 13)
├── 91-94%   TCL & Transactions (COMMIT, ROLLBACK, SAVEPOINT) (STEP 14)
├── 94-96%   Oracle SQL & SQL*Plus (STEP 15)
└── 96-100%  PL/SQL (Variables, Loops, Procedures, Functions, Cursors, Triggers, Packages) 🔥 (STEP 16)
```

---

## 1️⃣ What is a Database Constraint?

* **Definition:** A constraint is a declarative rule defined on table columns to enforce data accuracy, integrity, and consistency across database operations.
* **Purpose:** Prevents invalid, duplicate, orphaned, or out-of-range data from entering the database.
* **Enforcement Level:** Constraints are enforced automatically by the RDBMS engine during `INSERT`, `UPDATE`, and `DELETE` queries.

---

## 📊 Summary of SQL Constraints

| Constraint | Primary Rule / Description | Allows NULL? | Multiple per Table? |
| :--- | :--- | :--- | :--- |
| **`NOT NULL`** | Column cannot hold `NULL` values. | ❌ No | ✅ Yes |
| **`UNIQUE`** | All non-null values in the column must be unique. | ✅ Yes | ✅ Yes |
| **`PRIMARY KEY`** | Uniquely identifies each row (`NOT NULL` + `UNIQUE`). | ❌ No | ❌ No (Max 1 per table) |
| **`FOREIGN KEY`** | Links column to Primary Key of another parent table. | ✅ Yes | ✅ Yes |
| **`CHECK`** | Validates value against a logical expression. | ✅ Yes | ✅ Yes |
| **`DEFAULT`** | Assigns a fallback value if no value is supplied. | N/A | ✅ Yes |

---

## 2️⃣ Column-Level vs Table-Level Constraints

* **Column-Level Constraint:** Defined inline alongside a single column declaration.
* **Table-Level Constraint:** Defined at the end of table creation syntax. Required when creating composite keys spanning multiple columns.

```sql
CREATE TABLE employees (
    -- Column-level constraints:
    emp_id INT CONSTRAINT pk_emp PRIMARY KEY,
    email VARCHAR(100) CONSTRAINT uk_email UNIQUE,
    salary DECIMAL(10, 2) CONSTRAINT chk_sal CHECK (salary > 0),
    department_id INT,
    
    -- Table-level constraint (Foreign Key):
    CONSTRAINT fk_dept FOREIGN KEY (department_id) 
        REFERENCES departments(department_id)
);
```

---

## 🔍 Detailed Breakdown of Key Constraints

### 1️⃣ `PRIMARY KEY`
Uniquely identifies each record.
* Cannot contain duplicate values.
* Cannot contain `NULL`.

#### Composite Primary Key Example (Table-Level):
A single primary key composed of two or more columns:
```sql
CREATE TABLE student_courses (
    student_id INT,
    course_id INT,
    enrollment_date DATE,
    CONSTRAINT pk_student_course PRIMARY KEY (student_id, course_id)
);
```

---

### 2️⃣ `FOREIGN KEY` & Referential Integrity ⭐
A Foreign Key establishes a logical connection between a **child table** column and the **Primary Key** of a **parent table**.

```sql
-- Parent Table:
CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50) NOT NULL
);

-- Child Table:
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50) NOT NULL,
    dept_id INT,
    CONSTRAINT fk_emp_dept FOREIGN KEY (dept_id) 
        REFERENCES departments(dept_id)
);
```

#### 🔄 Foreign Key Deletion Behaviors (`ON DELETE` Rules):
What happens to child records when a parent record is deleted?

1. **`ON DELETE RESTRICT` / `NO ACTION` (Default):**
   Blocks deletion of parent row if child rows reference it.
2. **`ON DELETE CASCADE`:**
   Deletes all referencing child records automatically when parent row is deleted.
   ```sql
   CONSTRAINT fk_emp_dept FOREIGN KEY (dept_id) 
       REFERENCES departments(dept_id) ON DELETE CASCADE
   ```
3. **`ON DELETE SET NULL`:**
   Sets the child table's Foreign Key column to `NULL` when parent row is deleted.
   ```sql
   CONSTRAINT fk_emp_dept FOREIGN KEY (dept_id) 
       REFERENCES departments(dept_id) ON DELETE SET NULL
   ```

---

### 3️⃣ `CHECK` Constraint
Enforces custom domain logic rules on column values.

```sql
CREATE TABLE accounts (
    account_id INT PRIMARY KEY,
    account_type VARCHAR(20) CHECK (account_type IN ('SAVINGS', 'CHECKING', 'CREDIT')),
    balance DECIMAL(12, 2) CHECK (balance >= 0)
);
```

---

### 4️⃣ `DEFAULT` Constraint
Provides a default literal or system value when `INSERT` omits a value for the column.

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    order_date DATE DEFAULT SYSDATE,
    status VARCHAR(20) DEFAULT 'PENDING'
);
```

---

## 3️⃣ Managing Constraints via `ALTER TABLE`

### 1. Add a Constraint to an Existing Table:
```sql
ALTER TABLE employees 
ADD CONSTRAINT uk_emp_phone UNIQUE (phone_number);

ALTER TABLE employees 
ADD CONSTRAINT chk_emp_age CHECK (age >= 18);
```

### 2. Drop a Constraint:
```sql
-- Oracle / PostgreSQL:
ALTER TABLE employees DROP CONSTRAINT uk_emp_phone;

-- MySQL:
ALTER TABLE employees DROP INDEX uk_emp_phone;
```

---

## 🎯 STEP 9 — Practice Questions

1. **Question 1:** What is the primary difference between a `PRIMARY KEY` and a `UNIQUE` constraint?
2. **Question 2:** If table `Orders` references table `Customers(customer_id)` with `ON DELETE CASCADE`, what happens when customer `ID = 5` is deleted from `Customers`?
3. **Question 3:** Write a `CREATE TABLE` query for `products` with columns `product_id` (Primary Key), `product_name` (Cannot be NULL), `price` (Must be > 0), and `stock` (Default value `0`).
4. **Question 4:** How do you add a foreign key constraint to an existing table using `ALTER TABLE`?

---

## ⏩ Navigation
* ⏪ **Previous Step:** **[Step 08 — Functions, GROUP BY & HAVING](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_08_Functions_GROUP_BY_HAVING.md)**
* ⏩ **Next Step:** **[Step 10 — JOINS](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_10_JOINS.md)** — Master combining data across related tables!

