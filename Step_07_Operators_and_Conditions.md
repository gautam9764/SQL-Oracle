# 📘 STEP 7 — Operators & Conditions (45% → 50%)

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
├── 45-50%   Operators & Conditions (STEP 7) 👈 (You are here)
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

## 1️⃣ What are SQL Operators?

* **Definition:** An operator is a reserved character or keyword used in SQL statements to perform arithmetic calculations, string manipulations, comparison checks, and logical evaluations within expressions and conditions.
* **Categories:**
  1. Arithmetic Operators
  2. Relational / Comparison Operators
  3. Logical Operators (`AND`, `OR`, `NOT`)
  4. Special Conditional Operators (`IN`, `BETWEEN`, `LIKE`, `IS NULL`, `EXISTS`)

---

## 2️⃣ Arithmetic Operators

Used to perform mathematical computations on numeric data columns or literal values.

| Operator | Operation | Example | Output (`salary = 50000`) |
| :--- | :--- | :--- | :--- |
| **`+`** | Addition | `salary + 5000` | `55000` |
| **`-`** | Subtraction | `salary - 2000` | `48000` |
| **`*`** | Multiplication | `salary * 1.10` | `55000` (10% bonus) |
| **`/`** | Division | `salary / 12` | `4166.66` (Monthly salary) |
| **`%` / `MOD`** | Modulus (Remainder) | `MOD(10, 3)` | `1` |

---

## 3️⃣ Comparison / Relational Operators

Used to compare two expressions. Evaluates to `TRUE`, `FALSE`, or `UNKNOWN` (when `NULL` is involved).

| Operator | Meaning | Example Query |
| :--- | :--- | :--- |
| **`=`** | Equal to | `SELECT * FROM emp WHERE dept_id = 10;` |
| **`!=` or `<>`** | Not equal to | `SELECT * FROM emp WHERE status <> 'INACTIVE';` |
| **`>`** | Greater than | `SELECT * FROM emp WHERE salary > 60000;` |
| **`<`** | Less than | `SELECT * FROM emp WHERE age < 30;` |
| **`>=`** | Greater than or equal to | `SELECT * FROM emp WHERE experience >= 5;` |
| **`<=`** | Less than or equal to | `SELECT * FROM emp WHERE rating <= 3;` |

---

## 4️⃣ Logical Operators (`AND`, `OR`, `NOT`)

Used to combine multiple search conditions in a `WHERE` or `HAVING` clause.

### 1. `AND` Operator
Returns `TRUE` **only if both** conditions are true.
```sql
SELECT * FROM employees 
WHERE department_id = 20 AND salary > 50000;
```

### 2. `OR` Operator
Returns `TRUE` if **at least one** condition is true.
```sql
SELECT * FROM employees 
WHERE city = 'Mumbai' OR city = 'Delhi';
```

### 3. `NOT` Operator
Reverses / negates the truth value of a condition.
```sql
SELECT * FROM employees 
WHERE NOT (department_id = 10);
```

---

## 5️⃣ Special SQL Operators ⭐

### 1️⃣ `IN` & `NOT IN` (List Matching)
Replaces multiple `OR` conditions by checking if a column value matches any item in a list or subquery.

```sql
-- Equivalent to: city = 'Rajkot' OR city = 'Surat' OR city = 'Mumbai'
SELECT * FROM students 
WHERE city IN ('Rajkot', 'Surat', 'Mumbai');

-- Excluding items:
SELECT * FROM students 
WHERE city NOT IN ('Delhi', 'Kolkata');
```

---

### 2️⃣ `BETWEEN ... AND ...` (Range Check)
Filters records within an inclusive range (inclusive of boundary values).

```sql
-- Selects employees with salary between 40,000 and 80,000 inclusive
SELECT first_name, salary 
FROM employees 
WHERE salary BETWEEN 40000 AND 80000;
```

---

### 3️⃣ `LIKE` & Wildcard Characters (Pattern Matching)
Used for partial text searching in string columns.

#### 🔤 Wildcard Characters:
* **`%` (Percent):** Matches **zero, one, or multiple** characters.
* **`_` (Underscore):** Matches **exactly one single** character.

| Pattern | Meaning / Matches | Example Matches |
| :--- | :--- | :--- |
| **`'A%'`** | Starts with letter 'A' | 'Alice', 'Amit', 'A' |
| **`'%son'`** | Ends with 'son' | 'Jackson', 'Wilson' |
| **`'%ar%'`** | Contains 'ar' anywhere | 'Darshan', 'Rahul', 'Farhan' |
| **`'_a%'`** | Second letter is 'a' | 'Rahul', 'David', 'Karan' |
| **`'___'`** | Exactly 3 characters long | 'Bob', 'Tom', 'Sam' |

```sql
SELECT * FROM employees WHERE first_name LIKE 'J%';
```

---

### 4️⃣ `IS NULL` & `IS NOT NULL` (Handling Missing Data)
`NULL` represents missing or unknown data. **Never compare `NULL` using `=` or `!=`** (e.g., `col = NULL` evaluates to UNKNOWN). Always use `IS NULL`.

```sql
-- Find employees without an assigned manager:
SELECT first_name FROM employees WHERE manager_id IS NULL;

-- Find employees with a commission:
SELECT first_name, commission_pct FROM employees WHERE commission_pct IS NOT NULL;
```

---

## ⚡ Operator Precedence Rule

When combining multiple operators, SQL evaluates conditions in this order:

1. Parentheses `()`
2. Arithmetic Operators (`*`, `/`, `+`, `-`)
3. Comparison Operators (`=`, `>`, `<`, `LIKE`, `IN`, `BETWEEN`)
4. `IS NULL` / `IS NOT NULL`
5. `NOT`
6. `AND`
7. `OR`

> [!TIP]
> **Best Practice:** Use parentheses `()` explicitly when combining `AND` and `OR` to avoid logic errors.

```sql
-- Clear logic using parentheses:
SELECT * FROM employees 
WHERE (department_id = 10 OR department_id = 20) 
  AND salary > 50000;
```

---

## 🎯 STEP 7 — Practice Questions

1. **Question 1:** Write a query to find all employees whose `first_name` starts with `'M'` and ends with `'a'`.
2. **Question 2:** Why does `SELECT * FROM employees WHERE commission_pct = NULL;` fail to return rows with missing commission values? What is the correct query?
3. **Question 3:** Write a query using `BETWEEN` to retrieve employees hired between `'2022-01-01'` and `'2024-12-31'`.
4. **Question 4:** Convert this query into an equivalent query using `IN`:  
   `SELECT * FROM products WHERE category_id = 1 OR category_id = 4 OR category_id = 7;`

---

## ⏩ Navigation
* ⏪ **Previous Step:** **[Step 06 — DQL Commands](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_06_DQL_Commands.md)**
* ⏩ **Next Step:** **[Step 08 — Functions, GROUP BY & HAVING](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_08_Functions_GROUP_BY_HAVING.md)** — Learn built-in functions, data aggregation, and grouping!

