# 📘 STEP 11 — Subqueries Masterclass (78% → 83%)

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
├── 78-83%   Subqueries (STEP 11) 👈 (You are here)
├── 83-88%   Views + Index + Sequence + Synonym (STEP 12)
├── 88-91%   DCL Commands (GRANT, REVOKE) (STEP 13)
├── 91-94%   TCL & Transactions (COMMIT, ROLLBACK, SAVEPOINT) (STEP 14)
├── 94-96%   Oracle SQL & SQL*Plus (STEP 15)
└── 96-100%  PL/SQL (Variables, Loops, Procedures, Functions, Cursors, Triggers, Packages) 🔥 (STEP 16)
```

---

## 1️⃣ What is a Subquery?

* **Definition:** A subquery (or nested query / inner query) is a `SELECT` statement embedded inside another SQL query (`SELECT`, `INSERT`, `UPDATE`, or `DELETE`).
* **Execution Flow:** In standard subqueries, the inner subquery executes **first**, and its result is passed as an input parameter to the outer parent query.

```sql
-- Subquery example:
SELECT first_name, salary
FROM employees
WHERE salary > (
    -- Inner subquery (returns average salary value):
    SELECT AVG(salary) FROM employees
);
```

---

## 📊 Subquery Classification

Subqueries are classified based on:
1. **Output Structure:** Single-row, Multi-row, Multi-column.
2. **Coupling with Outer Query:** Independent Subquery vs Correlated Subquery.

---

## 🔍 Detailed Breakdown of Subquery Types

### 1️⃣ Single-Row Subquery
Returns **exactly one row and one column** (a scalar value).
* **Valid Comparison Operators:** `=`, `>`, `<`, `>=`, `<=`, `<>`.

```sql
-- Find employees who work in the same department as employee 101:
SELECT first_name, department_id
FROM employees
WHERE department_id = (
    SELECT department_id 
    FROM employees 
    WHERE employee_id = 101
);
```

---

### 2️⃣ Multi-Row Subquery
Returns **multiple rows** of data.
* **Valid Multi-Row Operators:** `IN`, `NOT IN`, `ANY` / `SOME`, `ALL`.

#### 1. `IN` Operator:
```sql
SELECT first_name, salary, department_id
FROM employees
WHERE department_id IN (
    SELECT department_id 
    FROM departments 
    WHERE location_id = 1700
);
```

#### 2. `ANY` / `SOME` Operator:
Compares a value against *any single item* in the returned list.
```sql
-- Selects employees earning more than AT LEAST ONE IT department employee:
SELECT first_name, salary
FROM employees
WHERE salary > ANY (
    SELECT salary FROM employees WHERE department_id = 60
);
```

#### 3. `ALL` Operator:
Compares a value against *every single item* in the returned list.
```sql
-- Selects employees earning more than ALL employees in department 60:
SELECT first_name, salary
FROM employees
WHERE salary > ALL (
    SELECT salary FROM employees WHERE department_id = 60
);
```

---

### 3️⃣ Subqueries in `FROM` Clause (Inline Views)
A subquery placed in the `FROM` clause acts as a temporary virtual table.

```sql
SELECT dept_summary.department_id, dept_summary.avg_sal
FROM (
    SELECT department_id, AVG(salary) AS avg_sal
    FROM employees
    GROUP BY department_id
) dept_summary
WHERE dept_summary.avg_sal > 60000;
```

---

### 4️⃣ Correlated Subquery ⭐
A subquery that **references a column from the outer query table**. Unlike normal subqueries, a correlated subquery executes **repeatedly**, once for every candidate row evaluated by the outer query.

```sql
-- Find employees who earn MORE than the average salary of THEIR OWN department:
SELECT e.first_name, e.salary, e.department_id
FROM employees e
WHERE e.salary > (
    SELECT AVG(salary)
    FROM employees d
    WHERE d.department_id = e.department_id  -- Correlated reference!
);
```

---

### 5️⃣ `EXISTS` & `NOT EXISTS` Operators
Evaluates to `TRUE` if the subquery returns **at least one row**. Optimizes execution because processing stops as soon as a single match is found.

```sql
-- Select departments that have at least one employee:
SELECT d.department_name
FROM departments d
WHERE EXISTS (
    SELECT 1 
    FROM employees e 
    WHERE e.department_id = d.department_id
);
```

---

## ⚡ `EXISTS` vs `IN` Comparison

| Feature | `EXISTS` Operator | `IN` Operator |
| :--- | :--- | :--- |
| **Evaluates** | Presence of matching rows (`TRUE`/`FALSE`). Short-circuits on 1st match. | Literal column value matching against list. |
| **`NULL` Behavior** | Handles `NULL` safely without unexpected empty sets. | If inner query returns a `NULL`, `NOT IN` returns 0 rows! |
| **Best Performance** | Faster when inner table is **large**. | Faster when inner result set is **small / fixed list**. |

---

## 🎯 STEP 11 — Practice Questions

1. **Question 1:** Write a subquery to find the employee(s) with the absolute **highest salary** in the `employees` table.
2. **Question 2:** Why does `SELECT * FROM emp WHERE dept_id NOT IN (SELECT dept_id FROM dept);` fail to return any rows if `dept` contains even a single `NULL` value?
3. **Question 3:** What is a correlated subquery, and how does its execution mechanism differ from an un-correlated subquery?
4. **Question 4:** Write a query using `EXISTS` to find customers who have placed at least one order.

---

## ⏩ Navigation
* ⏪ **Previous Step:** **[Step 10 — JOINS Masterclass](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_10_JOINS.md)**
* ⏩ **Next Step:** **[Step 12 — Views, Indexes, Sequences & Synonyms](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_12_Views_Index_Sequence_Synonym.md)** — Learn essential database schema objects!

