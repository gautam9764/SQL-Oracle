# 📘 STEP 4 — DDL Commands (15% → 25%)

---

## 🏆 SQL 0% → 100% Roadmap

```text
SQL
│
├── 0-5%     Database Fundamentals (STEP 1)
├── 5-10%    SQL Introduction & CRUD (STEP 2)
├── 10-15%   Data Types (STEP 3)
├── 15-25%   DDL Commands (STEP 4) 👈 (You are here)
├── 25-35%   DML Commands (STEP 5)
├── 35-45%   DQL Commands / SELECT + WHERE (STEP 6)
├── 45-50%   Operators & Conditions (STEP 7)
├── 50-60%   Functions + GROUP BY + HAVING (STEP 8)
├── 60-68%   Constraints (STEP 9)
├── 68-78%   JOINS (INNER, LEFT, RIGHT, FULL, CROSS, SELF) ⭐ (STEP 10)
├── 78-83%   Subqueries (STEP 11)
├── 83-88%   Views + Index + Sequence + Synonym (STEP 12)
├── 88-91%   DCL Commands (GRANT, REVOKE) (STEP 13)
├── 91-94%   TCL & Transactions (COMMIT, ROLLBACK, SAVEPOINT) (STEP 14)
├── 94-96%   Oracle SQL & SQL*Plus (STEP 15)
└── 96-100%  PL/SQL (Variables, Loops, Procedures, Functions, Cursors, Triggers, Packages) 🔥 (STEP 16)
```

---

## 1️⃣ What is DDL (Data Definition Language)?

* **Definition:** Data Definition Language (DDL) consists of SQL commands used to define, modify, and manage the **structure** or **schema** of database objects (such as tables, views, indexes, and schemas).
* **Key Characteristics:**
  1. **Structure Focus:** DDL commands operate on table structures, not individual data rows.
  2. **Auto-Commit:** In most RDBMS engines (like Oracle and MySQL), DDL commands are **auto-committed** immediately and cannot be undone using `ROLLBACK`.
* **5 Core DDL Commands:**
  * `CREATE` → Creates a new database object (table, view, index).
  * `ALTER` → Modifies the structure of an existing database object.
  * `DROP` → Permanently deletes an entire database object and its data.
  * `TRUNCATE` → Removes all rows from a table while preserving the table structure.
  * `RENAME` → Changes the name of an existing table or column.

---

## 2️⃣ CREATE Statement

The `CREATE` statement defines a new table structure, specifying column names, data types, and initial constraints.

### Syntax:
```sql
CREATE TABLE table_name (
    column1_name data_type [constraint],
    column2_name data_type [constraint],
    ...
    PRIMARY KEY (column1_name)
);
```

### Example: Creating an `employees` Table
```sql
CREATE TABLE employees (
    emp_id      INT,
    first_name  VARCHAR(50),
    last_name   VARCHAR(50),
    email       VARCHAR(100),
    hire_date   DATE,
    salary      DECIMAL(10, 2),
    PRIMARY KEY (emp_id)
);
```

---

## 3️⃣ ALTER Statement

The `ALTER` statement modifies the structure of an existing table without deleting its contents.

### 1. Adding a New Column (`ADD`)
```sql
ALTER TABLE employees 
ADD department_id INT;
```

### 2. Modifying an Existing Column (`MODIFY` / `ALTER COLUMN`)
* **Oracle / MySQL:** `MODIFY`
  ```sql
  ALTER TABLE employees 
  MODIFY salary DECIMAL(12, 2);
  ```
* **PostgreSQL / SQL Server:** `ALTER COLUMN`
  ```sql
  ALTER TABLE employees 
  ALTER COLUMN salary TYPE DECIMAL(12, 2);
  ```

### 3. Dropping a Column (`DROP COLUMN`)
```sql
ALTER TABLE employees 
DROP COLUMN email;
```

### 4. Renaming a Column (`RENAME COLUMN`)
```sql
ALTER TABLE employees 
RENAME COLUMN hire_date TO joining_date;
```

---

## 4️⃣ RENAME Statement

Used to rename an entire table object.

### Syntax & Example:
```sql
-- ANSI Standard / Oracle / MySQL
RENAME employees TO staff;

-- Alternative syntax in MySQL / PostgreSQL
ALTER TABLE employees RENAME TO staff;
```

---

## 5️⃣ TRUNCATE vs DROP vs DELETE ⭐

Understanding the difference between `TRUNCATE`, `DROP`, and `DELETE` is a critical database concept and a very frequent interview question.

| Feature | `TRUNCATE` | `DROP` | `DELETE` |
| :--- | :--- | :--- | :--- |
| **Command Category** | **DDL** (Data Definition) | **DDL** (Data Definition) | **DML** (Data Manipulation) |
| **Action** | Deletes **all rows** from table | Deletes **entire table structure** and data | Deletes **specific or all rows** |
| **Table Structure** | Preserved (empty table remains) | Destroyed (table no longer exists) | Preserved |
| **`WHERE` Clause Support?** | ❌ No | ❌ No | ✅ Yes |
| **Speed / Performance** | Very Fast (deallocates pages) | Very Fast | Slower (logs row by row) |
| **Rollback Capability** | Cannot be rolled back (Auto-commit) | Cannot be rolled back (Auto-commit) | Can be rolled back (TCL dependent) |
| **Storage Recovery** | Reclaims allocated space | Reclaims allocated space | Does not immediately reclaim space |

### Example Comparison:
```sql
-- TRUNCATE: Empties the table completely, table definition stays
TRUNCATE TABLE employees;

-- DROP: Completely removes the employees table from the database
DROP TABLE employees;

-- DELETE: Deletes specific rows where department_id is 10
DELETE FROM employees WHERE department_id = 10;
```

---

## 🎯 STEP 4 — Practice Questions

1. **Question 1:** Which DDL command is used to add a new column to an existing database table?
2. **Question 2:** Explain the key differences between `DROP TABLE` and `TRUNCATE TABLE`.
3. **Question 3:** Why can't a `TRUNCATE TABLE` command be reversed using `ROLLBACK` in most database engines?
4. **Question 4:** Write an SQL DDL query to create a table named `products` with columns `product_id` (Primary Key, INT), `product_name` (VARCHAR 100), and `price` (DECIMAL 8, 2).

---

## ⏩ Navigation
* ⏪ **Previous Step:** **[Step 03 — Data Types](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_03_Data_Types.md)**
* ⏩ **Next Step:** **[Step 05 — DML Commands](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_05_DML_Commands.md)** — Learn how to insert, update, delete, and merge data rows!

