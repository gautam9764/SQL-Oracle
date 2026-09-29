# 📘 STEP 6 — DQL Commands (35% → 45%)

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
├── 35-45%   DQL Commands / SELECT + WHERE (STEP 6) 👈 (You are here)
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

## 1️⃣ What is DQL (Data Query Language)?

* **Definition:** Data Query Language (DQL) consists of SQL statements used to retrieve, search, and fetch data stored in database tables without modifying any underlying data or table structures.
* **Core DQL Command:** **`SELECT`**
* **Execution Flow:** A `SELECT` query instructs the database engine to fetch specified attributes (columns) from one or more relations (tables) that satisfy specified criteria (conditions).

---

## 2️⃣ The `SELECT` Statement

### 1. Fetching All Columns (`SELECT *`)
Retrieves every column and row from the specified table.
```sql
SELECT * FROM employees;
```

### 2. Fetching Specific Columns
Improves performance and network payload by retrieving only necessary fields.
```sql
SELECT emp_id, first_name, salary FROM employees;
```

### 3. Column Aliases (`AS`)
Renames output column headers in the result set for display readability.
```sql
SELECT 
    first_name AS "First Name", 
    salary AS "Monthly Salary", 
    salary * 12 AS "Annual Compensation"
FROM employees;
```

---

## 3️⃣ Eliminating Duplicates (`DISTINCT`)

The `DISTINCT` keyword removes duplicate rows from the query result set, returning only unique values.

### Example: Finding Unique Cities or Departments
```sql
-- Returns only unique department IDs from employees table
SELECT DISTINCT department_id FROM employees;

-- Returns unique combinations of department and job title
SELECT DISTINCT department_id, job_title FROM employees;
```

---

## 4️⃣ Filtering Records (`WHERE` Clause)

The `WHERE` clause filters records so that only rows meeting specified conditional criteria are returned.

### Syntax:
```sql
SELECT column1, column2 
FROM table_name 
WHERE condition;
```

### Examples:
```sql
-- Filtering numeric ranges
SELECT first_name, salary 
FROM employees 
WHERE salary >= 60000;

-- Filtering string matches
SELECT first_name, last_name 
FROM employees 
WHERE city = 'Rajkot';
```

---

## 5️⃣ Sorting Results (`ORDER BY`)

The `ORDER BY` clause sorts the result set in ascending (`ASC`) or descending (`DESC`) order based on one or more columns. Default sorting order is `ASC`.

### 1. Single-Column Sort
```sql
SELECT first_name, salary 
FROM employees 
ORDER BY salary DESC;
```

### 2. Multi-Column Sort
Sorts primarily by `department_id` in ascending order, and secondarily by `salary` in descending order:
```sql
SELECT department_id, first_name, salary 
FROM employees 
ORDER BY department_id ASC, salary DESC;
```

---

## 6️⃣ Result Pagination & Limit Clauses

When working with large tables, returning millions of rows degrades application performance. Pagination limits the number of rows returned.

### 1. ANSI SQL Standard / Oracle 12c+ (`OFFSET ... FETCH`)
```sql
SELECT emp_id, first_name, salary 
FROM employees 
ORDER BY salary DESC 
OFFSET 0 ROWS FETCH FIRST 5 ROWS ONLY;
```

### 2. MySQL / PostgreSQL (`LIMIT ... OFFSET`)
```sql
SELECT emp_id, first_name, salary 
FROM employees 
ORDER BY salary DESC 
LIMIT 5 OFFSET 0;
```

### 3. Oracle 11g and earlier (`ROWNUM`)
```sql
SELECT * FROM (
    SELECT emp_id, first_name, salary 
    FROM employees 
    ORDER BY salary DESC
) WHERE ROWNUM <= 5;
```

---

## 💡 SQL SELECT Clause Execution Order ⭐

Although we write SQL queries in a specific order, the database engine processes clauses in a completely different sequence:

```text
Writing Order:             Execution Order (Database Engine):
1. SELECT                  1. FROM       (Identify table)
2. FROM                    2. WHERE      (Filter rows)
3. WHERE                   3. GROUP BY   (Group rows)
4. GROUP BY                4. HAVING     (Filter groups)
5. HAVING                  5. SELECT     (Project columns & expressions)
6. ORDER BY                6. DISTINCT   (Remove duplicates)
7. LIMIT / FETCH           7. ORDER BY   (Sort output)
                           8. LIMIT      (Paginate output)
```

---

## 🎯 STEP 6 — Practice Questions

1. **Question 1:** What is the difference between `SELECT *` and specifying column names explicitly?
2. **Question 2:** In what order does a database engine process `FROM`, `WHERE`, `SELECT`, and `ORDER BY`?
3. **Question 3:** Write an SQL query to retrieve unique job titles from the `employees` table where salary is greater than `50000`, sorted alphabetically by job title.
4. **Question 4:** How do you fetch the top 3 highest-earning employees using ANSI SQL `FETCH FIRST` syntax?

---

## ⏩ Navigation
* ⏪ **Previous Step:** **[Step 05 — DML Commands](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_05_DML_Commands.md)**
* ⏩ **Next Step:** **[Step 07 — Operators & Conditions](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_07_Operators_and_Conditions.md)** — Master arithmetic, logical, and filtering operators (`IN`, `BETWEEN`, `LIKE`, `IS NULL`)!

