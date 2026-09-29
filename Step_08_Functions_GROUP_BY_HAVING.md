# 📘 STEP 8 — Functions, GROUP BY & HAVING (50% → 60%)

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
├── 50-60%   Functions + GROUP BY + HAVING (STEP 8) 👈 (You are here)
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

## 1️⃣ SQL Functions Classification

SQL functions are built-in operations that accept inputs, process data, and return a result. They are divided into **2 main categories**:

```text
SQL Functions
├── 1. Single-Row (Scalar) Functions  → Acts on 1 row at a time (Returns 1 output per row)
└── 2. Multiple-Row (Aggregate) Functions → Acts on a group of rows (Returns 1 output per group)
```

---

## 2️⃣ Single-Row (Scalar) Functions

### 🔤 1. String Functions

| Function | Purpose | Example | Output |
| :--- | :--- | :--- | :--- |
| **`UPPER(str)`** | Converts string to uppercase | `UPPER('oracle')` | `'ORACLE'` |
| **`LOWER(str)`** | Converts string to lowercase | `LOWER('SQL')` | `'sql'` |
| **`LENGTH(str)`** | Returns character length | `LENGTH('Database')` | `8` |
| **`SUBSTR(str, pos, len)`** | Extracts substring starting at `pos` | `SUBSTR('Database', 1, 4)` | `'Data'` |
| **`CONCAT(str1, str2)`** | Joins two text strings | `CONCAT('Hello ', 'World')` | `'Hello World'` |
| **`TRIM(str)`** | Removes leading/trailing spaces | `TRIM('  sql  ')` | `'sql'` |
| **`REPLACE(str, search, rep)`**| Replaces occurrences of substring | `REPLACE('Cat', 'C', 'B')` | `'Bat'` |
| **`INSTR(str, sub)`** | Returns 1st position of substring | `INSTR('Oracle', 'c')` | `4` |

---

### 🔢 2. Numeric Functions

| Function | Purpose | Example | Output |
| :--- | :--- | :--- | :--- |
| **`ROUND(num, dec)`** | Rounds number to `dec` decimal places | `ROUND(45.678, 2)` | `45.68` |
| **`TRUNC(num, dec)`** | Truncates digits without rounding | `TRUNC(45.678, 2)` | `45.67` |
| **`MOD(m, n)`** | Returns remainder of `m / n` | `MOD(10, 3)` | `1` |
| **`ABS(num)`** | Returns absolute positive value | `ABS(-25)` | `25` |
| **`POWER(m, n)`** | Calculates `m` raised to power `n` | `POWER(2, 3)` | `8` |

---

### 📅 3. Date Functions

| Function | Purpose | Example / Syntax |
| :--- | :--- | :--- |
| **`SYSDATE` / `CURRENT_DATE`**| Returns current system date & time | `SELECT SYSDATE FROM DUAL;` |
| **`ADD_MONTHS(date, n)`** | Adds `n` months to a date | `ADD_MONTHS(SYSDATE, 3)` |
| **`MONTHS_BETWEEN(d1, d2)`** | Returns number of months between dates | `MONTHS_BETWEEN('01-JAN-24', '01-JAN-23')` → `12` |
| **`LAST_DAY(date)`** | Returns last day of the given month | `LAST_DAY(SYSDATE)` |
| **`EXTRACT(unit FROM date)`** | Extracts `YEAR`, `MONTH`, `DAY` component | `EXTRACT(YEAR FROM SYSDATE)` |

---

### 🛡️ 4. NULL Handling & Conditional Functions

#### `NVL(expr1, expr2)` (Oracle) / `IFNULL(expr1, expr2)` (MySQL)
If `expr1` is `NULL`, returns `expr2`. Otherwise returns `expr1`.
```sql
SELECT first_name, salary + NVL(commission_pct, 0) AS total_pay 
FROM employees;
```

#### `COALESCE(val1, val2, ... valN)` (ANSI Standard)
Returns the **first non-null value** in the argument list.
```sql
SELECT first_name, COALESCE(mobile_phone, home_phone, office_phone, 'No Phone') AS contact 
FROM contacts;
```

#### `CASE` Expression (Conditional Logic)
```sql
SELECT first_name, salary,
  CASE 
    WHEN salary >= 80000 THEN 'High Salary'
    WHEN salary >= 50000 THEN 'Medium Salary'
    ELSE 'Entry Level'
  END AS salary_grade
FROM employees;
```

---

## 3️⃣ Aggregate (Multi-Row) Functions

Aggregate functions take multiple values across rows and compute a single summary result.

| Aggregate Function | Description | Example |
| :--- | :--- | :--- |
| **`COUNT(*)`** | Counts total rows in a table (including NULLs). | `SELECT COUNT(*) FROM employees;` |
| **`COUNT(column)`** | Counts non-null entries in specific column. | `SELECT COUNT(commission_pct) FROM employees;` |
| **`SUM(column)`** | Calculates total sum of numeric values. | `SELECT SUM(salary) FROM employees;` |
| **`AVG(column)`** | Calculates average of numeric values. | `SELECT AVG(salary) FROM employees;` |
| **`MIN(column)`** | Finds minimum value (number, text, date). | `SELECT MIN(hire_date) FROM employees;` |
| **`MAX(column)`** | Finds maximum value (number, text, date). | `SELECT MAX(salary) FROM employees;` |

---

## 4️⃣ Data Grouping with `GROUP BY`

The `GROUP BY` clause divides rows into summary groups based on matching values in one or more columns, allowing aggregate functions to be evaluated per group.

```sql
SELECT department_id, COUNT(*) AS total_employees, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id;
```

> [!IMPORTANT]
> **Golden Rule of `GROUP BY`:**
> Any individual column listed in the `SELECT` clause **MUST** either be included in the `GROUP BY` clause or be wrapped inside an aggregate function!

```sql
-- ❌ INCORRECT (first_name is not grouped or aggregated):
SELECT department_id, first_name, AVG(salary) 
FROM employees 
GROUP BY department_id;

-- ✅ CORRECT:
SELECT department_id, AVG(salary) 
FROM employees 
GROUP BY department_id;
```

---

## 5️⃣ Filtering Groups with `HAVING`

The `HAVING` clause filters **grouped summary rows** generated by `GROUP BY`.

```sql
SELECT department_id, COUNT(*) AS total_staff, AVG(salary) AS avg_sal
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 5;
```

---

## ⚡ `WHERE` vs `HAVING` Comparison

| Feature | `WHERE` Clause | `HAVING` Clause |
| :--- | :--- | :--- |
| **Filtering Level** | Filters individual **rows** before grouping. | Filters summary **groups** after `GROUP BY`. |
| **Aggregate Functions** | ❌ Cannot contain aggregate functions (`WHERE SUM(sal) > 1000` is illegal). | ✅ Designed specifically for aggregate conditions (`HAVING AVG(sal) > 50000`). |
| **Position in SQL** | Appears **before** `GROUP BY`. | Appears **after** `GROUP BY`. |

---

## 🔄 Complete SQL Logical Execution Order ⭐

Understanding how the database engine executes SQL queries step-by-step:

```text
1. FROM       → Identifies target table(s)
2. WHERE      → Filters individual rows
3. GROUP BY   → Groups remaining rows
4. HAVING     → Filters aggregated groups
5. SELECT     → Evaluates projections & functions
6. DISTINCT   → Removes duplicates
7. ORDER BY   → Sorts final output set
8. LIMIT/FETCH→ Truncates total rows returned
```

---

## 🎯 STEP 8 — Practice Questions

1. **Question 1:** Write a query to display `department_id` and the total salary paid in each department, but only for departments where total salary exceeds `200,000`.
2. **Question 2:** What is the difference between `COUNT(*)` and `COUNT(commission_pct)` when `commission_pct` contains `NULL` values?
3. **Question 3:** What is the output of `ROUND(157.348, -1)` and `ROUND(157.348, 1)`?
4. **Question 4:** Explain why `SELECT dept_id, AVG(salary) FROM emp WHERE AVG(salary) > 5000 GROUP BY dept_id;` throws a syntax error, and rewrite it correctly.

---

## ⏩ Navigation
* ⏪ **Previous Step:** **[Step 07 — Operators & Conditions](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_07_Operators_and_Conditions.md)**
* ⏩ **Next Step:** **[Step 09 — Constraints](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_09_Constraints.md)** — Enforce data rules and referential integrity!

