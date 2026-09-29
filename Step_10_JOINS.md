# 📘 STEP 10 — JOINS Masterclass ⭐ (68% → 78%)

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
├── 68-78%   JOINS (INNER, LEFT, RIGHT, FULL, CROSS, SELF) ⭐ 👈 (You are here)
├── 78-83%   Subqueries (STEP 11)
├── 83-88%   Views + Index + Sequence + Synonym (STEP 12)
├── 88-91%   DCL Commands (GRANT, REVOKE) (STEP 13)
├── 91-94%   TCL & Transactions (COMMIT, ROLLBACK, SAVEPOINT) (STEP 14)
├── 94-96%   Oracle SQL & SQL*Plus (STEP 15)
└── 96-100%  PL/SQL (Variables, Loops, Procedures, Functions, Cursors, Triggers, Packages) 🔥 (STEP 16)
```

---

## 1️⃣ What is an SQL JOIN?

* **Definition:** An SQL JOIN clause is used to query and combine columns from two or more tables based on a related logical column (usually Primary Key - Foreign Key relationships) between them.
* **Why JOINS are Essential:** In database design, data is normalized into separate tables to prevent redundancy. JOINS allow us to reconstruct comprehensive business views dynamically.

---

## 📊 Visual Venn Diagram Representation

```text
       INNER JOIN                     LEFT JOIN                   RIGHT JOIN
    ┌───────┬───────┐              ┌───────┬───────┐           ┌───────┬───────┐
    │ Table │ Matching│ Table │    │ Table │ Matching│ Table │   │ Table │ Matching│ Table │
    │   A   │ Rows  │   B   │      │   A   │ Rows  │   B   │     │   A   │ Rows  │   B   │
    │       │  (A∩B)│       │      │█ █ █ █│█ █ █ █│       │     │       │█ █ █ █│█ █ █ █│
    └───────┴───────┴───────┘      └───────┴───────┴───────┘   └───────┴───────┴───────┘
            (A ∩ B)                   (All A + Matching B)        (All B + Matching A)

                                      FULL OUTER JOIN
                                   ┌───────┬───────┬───────┐
                                   │ Table │ Matching│ Table │
                                   │   A   │ Rows  │   B   │
                                   │█ █ █ █│█ █ █ █│█ █ █ █│
                                   └───────┴───────┴───────┘
                                     (All Rows from A & B)
```

---

## 📁 Sample Tables for Examples

#### `employees` Table (Left Table):

| emp_id | emp_name | dept_id |
| :--- | :--- | :--- |
| **1** | Alice | 10 |
| **2** | Bob | 20 |
| **3** | Charlie | 20 |
| **4** | David | *NULL* |

#### `departments` Table (Right Table):

| dept_id | dept_name |
| :--- | :--- |
| **10** | IT |
| **20** | HR |
| **30** | Marketing |

---

## 🔍 Detailed Breakdown of JOIN Types

### 1️⃣ `INNER JOIN`
Returns only records that have **matching values in both tables**. Non-matching rows from both sides are excluded.

```sql
SELECT e.emp_id, e.emp_name, d.dept_name
FROM employees e
INNER JOIN departments d
  ON e.dept_id = d.dept_id;
```

#### Result Set:
| emp_id | emp_name | dept_name |
| :--- | :--- | :--- |
| **1** | Alice | IT |
| **2** | Bob | HR |
| **3** | Charlie | HR |

*(Note: David has NULL dept_id and Marketing has no employees, so both are excluded).*

---

### 2️⃣ `LEFT (OUTER) JOIN`
Returns **all records from the left table**, along with matching records from the right table. If there is no match, `NULL` values are returned for right table columns.

```sql
SELECT e.emp_id, e.emp_name, d.dept_name
FROM employees e
LEFT JOIN departments d
  ON e.dept_id = d.dept_id;
```

#### Result Set:
| emp_id | emp_name | dept_name |
| :--- | :--- | :--- |
| **1** | Alice | IT |
| **2** | Bob | HR |
| **3** | Charlie | HR |
| **4** | David | *NULL* |

---

### 3️⃣ `RIGHT (OUTER) JOIN`
Returns **all records from the right table**, along with matching records from the left table. Unmatched left columns return `NULL`.

```sql
SELECT e.emp_id, e.emp_name, d.dept_name
FROM employees e
RIGHT JOIN departments d
  ON e.dept_id = d.dept_id;
```

#### Result Set:
| emp_id | emp_name | dept_name |
| :--- | :--- | :--- |
| **1** | Alice | IT |
| **2** | Bob | HR |
| **3** | Charlie | HR |
| *NULL* | *NULL* | Marketing |

---

### 4️⃣ `FULL (OUTER) JOIN`
Returns **all records from both tables**, filling `NULL` for non-matching sides.

```sql
SELECT e.emp_id, e.emp_name, d.dept_name
FROM employees e
FULL JOIN departments d
  ON e.dept_id = d.dept_id;
```

#### Result Set:
| emp_id | emp_name | dept_name |
| :--- | :--- | :--- |
| **1** | Alice | IT |
| **2** | Bob | HR |
| **3** | Charlie | HR |
| **4** | David | *NULL* |
| *NULL* | *NULL* | Marketing |

---

### 5️⃣ `CROSS JOIN` (Cartesian Product)
Combines every row of the left table with every row of the right table. Total rows returned = `(Rows in Table A) × (Rows in Table B)`.

```sql
SELECT e.emp_name, d.dept_name
FROM employees e
CROSS JOIN departments d;
```

*(Output: 4 employees × 3 departments = 12 total output rows).*

---

### 6️⃣ `SELF JOIN`
A table joined to **itself** to evaluate hierarchical or recursive relationships (e.g., finding an employee's manager).

```sql
SELECT 
    e.emp_name AS "Employee", 
    m.emp_name AS "Manager"
FROM employees e
LEFT JOIN employees m
  ON e.manager_id = m.emp_id;
```

---

## ⚡ `ON` Clause vs `WHERE` Clause in Outer Joins

* **`ON` Clause Filtering:** Filters records **during** the join process before constructing outer join NULL rows.
* **`WHERE` Clause Filtering:** Filters records **after** the join result has already been evaluated, potentially turning a `LEFT JOIN` into an `INNER JOIN`.

```sql
-- Filters during join (Preserves unmatched employees with NULL dept):
SELECT e.emp_name, d.dept_name
FROM employees e
LEFT JOIN departments d
  ON e.dept_id = d.dept_id AND d.dept_name = 'IT';

-- Filters after join (Removes employees where dept_name IS NOT 'IT'):
SELECT e.emp_name, d.dept_name
FROM employees e
LEFT JOIN departments d
  ON e.dept_id = d.dept_id
WHERE d.dept_name = 'IT';
```

---

## 🎯 STEP 10 — Practice Questions

1. **Question 1:** Write a query to list all department names that have **zero** assigned employees.
2. **Question 2:** If Table A has 5 rows and Table B has 10 rows, how many rows will a `CROSS JOIN` produce?
3. **Question 3:** What is a `SELF JOIN`, and what column structure is required in a table to perform it?
4. **Question 4:** Rewrite the following legacy Oracle outer join syntax using standard ANSI `LEFT JOIN` syntax:  
   `SELECT e.name, d.name FROM emp e, dept d WHERE e.dept_id = d.dept_id(+);`

---

## ⏩ Navigation
* ⏪ **Previous Step:** **[Step 09 — Constraints](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_09_Constraints.md)**
* ⏩ **Next Step:** **[Step 11 — Subqueries](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_11_Subqueries.md)** — Master nested queries!

