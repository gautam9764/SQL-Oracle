# 📘 STEP 5 — DML Commands (25% → 35%)

---

## 🏆 SQL 0% → 100% Roadmap

```text
SQL
│
├── 0-5%     Database Fundamentals (STEP 1)
├── 5-10%    SQL Introduction & CRUD (STEP 2)
├── 10-15%   Data Types (STEP 3)
├── 15-25%   DDL Commands (STEP 4)
├── 25-35%   DML Commands (STEP 5) 👈 (You are here)
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

## 1️⃣ What is DML (Data Manipulation Language)?

* **Definition:** Data Manipulation Language (DML) consists of SQL commands used to manage, manipulate, and modify the actual **data rows** stored inside database tables.
* **Key Characteristics:**
  1. **Row-Level Operations:** Operates directly on the contents of the database (records/tuples), not on the table definitions.
  2. **Transactional Safety:** DML operations can be saved (`COMMIT`) or undone (`ROLLBACK`) before they are permanently written to disk.
* **4 Primary DML Commands:**
  * `INSERT` → Adds new records to a table.
  * `UPDATE` → Modifies existing values in table rows.
  * `DELETE` → Removes specific or all records from a table.
  * `MERGE` (`UPSERT`) → Conditionally updates existing records or inserts new records.

---

## 2️⃣ INSERT Statement

The `INSERT INTO` statement is used to add new rows of data into a table.

### 1. Single-Row Insert
Explicitly specifying column names and corresponding values:
```sql
INSERT INTO employees (emp_id, first_name, last_name, salary, hire_date)
VALUES (101, 'Darshan', 'Patel', 75000.00, TO_DATE('2024-01-15', 'YYYY-MM-DD'));
```

### 2. Multi-Row Insert (Batch Insert)
Inserting multiple records in a single query:
```sql
INSERT INTO employees (emp_id, first_name, last_name, salary, hire_date)
VALUES 
    (102, 'Rahul', 'Sharma', 65000.00, TO_DATE('2024-02-01', 'YYYY-MM-DD')),
    (103, 'Priya', 'Mehta', 82000.00, TO_DATE('2024-03-10', 'YYYY-MM-DD')),
    (104, 'Amit', 'Verma', 58000.00, TO_DATE('2024-04-05', 'YYYY-MM-DD'));
```

### 3. Insert from Another Table (`INSERT INTO ... SELECT`)
Copying selected data from a source table into a target table:
```sql
INSERT INTO senior_employees (emp_id, first_name, last_name, salary)
SELECT emp_id, first_name, last_name, salary
FROM employees
WHERE salary > 70000;
```

---

## 3️⃣ UPDATE Statement

The `UPDATE` statement modifies values in existing table rows.

> [!WARNING]
> **CRITICAL WARNING:** Always use a `WHERE` clause when executing `UPDATE` statements! Omitting `WHERE` will update **every single row** in the table.

### 1. Updating a Single Column
```sql
UPDATE employees
SET salary = 80000.00
WHERE emp_id = 101;
```

### 2. Updating Multiple Columns simultaneously
```sql
UPDATE employees
SET salary = salary * 1.10,
    last_name = 'Trivedi'
WHERE emp_id = 102;
```

### 3. Conditional Update based on multiple criteria
```sql
UPDATE employees
SET salary = salary + 5000
WHERE salary < 60000 AND hire_date <= TO_DATE('2024-03-01', 'YYYY-MM-DD');
```

---

## 4️⃣ DELETE Statement

The `DELETE` statement removes existing rows from a table based on a specified condition.

> [!WARNING]
> **CRITICAL WARNING:** Omitting the `WHERE` clause in a `DELETE` command will delete **all records** from the table!

### 1. Conditional Deletion (Deleting Specific Rows)
```sql
DELETE FROM employees
WHERE emp_id = 104;
```

### 2. Deleting Rows Based on Complex Conditions
```sql
DELETE FROM employees
WHERE salary < 50000 OR hire_date IS NULL;
```

### 3. Deleting All Rows (Preserving Table Structure)
```sql
DELETE FROM employees;
```

---

## 5️⃣ MERGE / UPSERT Statement ⭐

The `MERGE` statement (also known as an **UPSERT** operation) combines `INSERT` and `UPDATE` into a single atomic command. It checks whether a record exists based on a matching key:
- If a match is found → Executed as an `UPDATE`.
- If no match is found → Executed as an `INSERT`.

### Syntax & Example (Oracle / Standard SQL):
```sql
MERGE INTO employees target
USING new_employee_data source
ON (target.emp_id = source.emp_id)
WHEN MATCHED THEN
    UPDATE SET 
        target.salary = source.salary,
        target.last_name = source.last_name
WHEN NOT MATCHED THEN
    INSERT (emp_id, first_name, last_name, salary, hire_date)
    VALUES (source.emp_id, source.first_name, source.last_name, source.salary, source.hire_date);
```

---

## 💡 DML Quick Summary Table

| DML Command | Primary Purpose | `WHERE` Clause Required? | Transactional Rollback? |
| :--- | :--- | :--- | :--- |
| **`INSERT`** | Creates new rows | ❌ No | ✅ Yes (`ROLLBACK`) |
| **`UPDATE`** | Modifies existing row values | ⚠️ Recommended (prevents updating all rows) | ✅ Yes (`ROLLBACK`) |
| **`DELETE`** | Removes specific data rows | ⚠️ Recommended (prevents wiping table) | ✅ Yes (`ROLLBACK`) |
| **`MERGE`** | Conditional Update / Insert | ✅ `ON (...)` matching condition | ✅ Yes (`ROLLBACK`) |

---

## 🎯 STEP 5 — Practice Questions

1. **Question 1:** What happens if you execute `UPDATE employees SET salary = 90000;` without a `WHERE` clause?
2. **Question 2:** How do you insert data into a table directly from another table using SQL?
3. **Question 3:** What is the primary advantage of the `MERGE` statement compared to separate `UPDATE` and `INSERT` queries?
4. **Question 4:** Write an SQL DML query to increase the salary of all employees in department `10` by `15%`.

---

## ⏩ Navigation
* ⏪ **Previous Step:** **[Step 04 — DDL Commands](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_04_DDL_Commands.md)**
* ⏩ **Next Step:** **[Step 06 — DQL Commands](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_06_DQL_Commands.md)** — Learn how to query and filter data using `SELECT`, `WHERE`, and pagination!

