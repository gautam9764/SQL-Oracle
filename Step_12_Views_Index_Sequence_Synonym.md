# 📘 STEP 12 — Database Objects: Views, Indexes, Sequences & Synonyms (83% → 88%)

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
├── 60-68%   Constraints (STEP 9)
├── 68-78%   JOINS (INNER, LEFT, RIGHT, FULL, CROSS, SELF) ⭐ (STEP 10)
├── 78-83%   Subqueries (STEP 11)
├── 83-88%   Views + Index + Sequence + Synonym (STEP 12) 👈 (You are here)
├── 88-91%   DCL Commands (GRANT, REVOKE) (STEP 13)
├── 91-94%   TCL & Transactions (COMMIT, ROLLBACK, SAVEPOINT) (STEP 14)
├── 94-96%   Oracle SQL & SQL*Plus (STEP 15)
└── 96-100%  PL/SQL (Variables, Loops, Procedures, Functions, Cursors, Triggers, Packages) 🔥 (STEP 16)
```

---

## 1️⃣ Views (Virtual Tables)

### What is a View?
* **Definition:** A View is a virtual, logical table based on the result set of a pre-written SQL `SELECT` query. A view does not store data rows itself (except Materialized Views); it dynamically reads data from base tables whenever queried.

### Key Benefits:
1. **Security:** Restricts direct user access to sensitive table columns (e.g., hiding passwords or salaries).
2. **Simplicity:** Encapsulates complex joins and subqueries into a simple `SELECT * FROM view_name;`.
3. **Data Independence:** Allows structural changes to base tables without breaking client application queries.

---

### Creating & Managing Views

#### 1. Create a Simple View:
```sql
CREATE VIEW emp_dept_10 AS
SELECT employee_id, first_name, salary, department_id
FROM employees
WHERE department_id = 10;
```

#### 2. Query a View:
```sql
SELECT * FROM emp_dept_10 WHERE salary > 30000;
```

#### 3. View with `WITH CHECK OPTION`:
Prevents DML operations through the view that violate the view's `WHERE` clause condition.
```sql
CREATE VIEW high_sal_emp AS
SELECT employee_id, first_name, salary
FROM employees
WHERE salary >= 50000
WITH CHECK OPTION;
```

#### 4. Drop a View:
```sql
DROP VIEW emp_dept_10;
```

---

### Simple Views vs Complex Views

| Feature | Simple View | Complex View |
| :--- | :--- | :--- |
| **Number of Tables** | Derived from **1 table** | Derived from **2+ joined tables** |
| **Contains Functions?**| ❌ No aggregate functions | ✅ Can contain aggregate functions |
| **Contains GROUP BY?** | ❌ No | ✅ Yes |
| **DML Operations?** | ✅ Allowed (Updates base table) | ❌ Restricted or Not Allowed |

---

## 2️⃣ Indexes (Performance Tuning) ⭐

### What is an Index?
* **Definition:** An Index is a database structure (typically built as a B-Tree) created on table columns to accelerate search and retrieval speed (`SELECT`), similar to an index at the back of a textbook.

### Benefits & Trade-offs:
* 🟢 **Pros:** Drastically speeds up `WHERE`, `JOIN`, `ORDER BY`, and `GROUP BY` operations.
* 🔴 **Cons:** Consumes additional storage space and slows down `INSERT`, `UPDATE`, and `DELETE` operations because the index must be updated on every write.

---

### Index Types & Syntax

#### 1. B-Tree Index (Standard Default):
```sql
CREATE INDEX idx_emp_lastname 
ON employees (last_name);
```

#### 2. Unique Index:
Guarantees uniqueness across column values while providing index lookup performance.
```sql
CREATE UNIQUE INDEX idx_emp_email 
ON employees (email);
```

#### 3. Composite (Multi-Column) Index:
```sql
CREATE INDEX idx_emp_dept_sal 
ON employees (department_id, salary);
```

#### 4. Drop an Index:
```sql
DROP INDEX idx_emp_lastname;
```

---

## 3️⃣ Sequences (Auto-Increment Generators)

### What is a Sequence?
* **Definition:** A Sequence is a database object used to generate unique, sequential numeric values automatically (commonly used to populate Primary Key columns like `order_id` or `user_id`).

### Creating a Sequence:
```sql
CREATE SEQUENCE emp_seq
    START WITH 1000
    INCREMENT BY 1
    MAXVALUE 999999
    NOCACHE
    NOCYCLE;
```

### Using Sequence Pseudo-Columns:
* **`NEXTVAL`:** Generates and returns the next sequential number.
* **`CURRVAL`:** Returns the current value generated in the current session.

```sql
INSERT INTO employees (employee_id, first_name, last_name)
VALUES (emp_seq.NEXTVAL, 'Darshan', 'Patel');
```

---

## 4️⃣ Synonyms (Object Aliases)

### What is a Synonym?
* **Definition:** A Synonym is an alternative name (alias) created for a database object such as a table, view, sequence, or procedure.
* **Purpose:** Hides underlying object ownership/location details and simplifies long schema table names (`hr.department_master_archive` → `depts`).

### Types of Synonyms:
1. **Private Synonym:** Accessible only by the schema owner or granted user.
2. **Public Synonym:** Accessible to all database users.

```sql
-- Create Private Synonym:
CREATE SYNONYM depts FOR hr.departments;

-- Create Public Synonym (Requires DBA privilege):
CREATE PUBLIC SYNONYM emp FOR hr.employees;

-- Drop Synonym:
DROP SYNONYM depts;
```

---

## 🎯 STEP 12 — Practice Questions

1. **Question 1:** Why should you avoid creating indexes on columns that undergo frequent `INSERT` and `DELETE` operations?
2. **Question 2:** Write a query to create a sequence named `order_seq` starting at `100` and incrementing by `10`.
3. **Question 3:** What is the difference between `NEXTVAL` and `CURRVAL` in database sequences?
4. **Question 4:** What is the primary purpose of creating a **Public Synonym** in Oracle SQL?

---

## ⏩ Navigation
* ⏪ **Previous Step:** **[Step 11 — Subqueries](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_11_Subqueries.md)**
* ⏩ **Next Step:** **[Step 13 — DCL Commands](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_13_DCL_Commands.md)** — Learn database security, user management, and privileges!

