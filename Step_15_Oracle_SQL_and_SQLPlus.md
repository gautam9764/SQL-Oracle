# 📘 STEP 15 — Oracle SQL & SQL*Plus (94% → 96%)

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
├── 83-88%   Views + Index + Sequence + Synonym (STEP 12)
├── 88-91%   DCL Commands (GRANT, REVOKE) (STEP 13)
├── 91-94%   TCL & Transactions (COMMIT, ROLLBACK, SAVEPOINT) (STEP 14)
├── 94-96%   Oracle SQL & SQL*Plus (STEP 15) 👈 (You are here)
└── 96-100%  PL/SQL (Variables, Loops, Procedures, Functions, Cursors, Triggers, Packages) 🔥 (STEP 16)
```

---

## 1️⃣ Oracle-Specific SQL Features

Oracle Database includes several powerful vendor-specific features and pseudo-columns that extend standard ANSI SQL.

### 1. The `DUAL` Table
`DUAL` is a special 1-row, 1-column dummy table automatically present in Oracle database schemas. It is used to evaluate functions, arithmetic calculations, or system constants without querying actual data tables.

```sql
-- Evaluate system date:
SELECT SYSDATE FROM DUAL;

-- Evaluate mathematical expression:
SELECT POWER(2, 10) AS result FROM DUAL;

-- Evaluate user session:
SELECT USER FROM DUAL;
```

---

### 2. Pseudo-Columns in Oracle

Pseudo-columns act like table columns, but are not stored in table definitions.

| Pseudo-Column | Description | Example Query |
| :--- | :--- | :--- |
| **`ROWNUM`** | Returns a number indicating the order in which Oracle selects the row. | `SELECT * FROM emp WHERE ROWNUM <= 5;` |
| **`ROWID`** | Physical binary disk address of a row (Fastest row access method in Oracle). | `SELECT ROWID, first_name FROM emp;` |
| **`USER`** | Name of the currently logged-in database user. | `SELECT USER FROM DUAL;` |
| **`SYSDATE`** | System timestamp of the database server. | `SELECT SYSDATE FROM DUAL;` |

> [!WARNING]
> **`ROWNUM` Pagination Caution:** `ROWNUM` is assigned **before** `ORDER BY` sorting occurs! To paginate sorted data properly, use subqueries or Oracle 12c+ `FETCH FIRST` clause.

---

### 3. Oracle 12c+ Modern Pagination Clause

```sql
SELECT employee_id, first_name, salary
FROM employees
ORDER BY salary DESC
OFFSET 10 ROWS FETCH NEXT 10 ROWS ONLY;
```

---

## 2️⃣ Mastering SQL*Plus Command Line Client

**SQL\*Plus** is the default command-line interface provided with Oracle Database for executing SQL and PL/SQL commands.

### 🔑 Connecting to Database:
```text
sqlplus hr/oracle@localhost:1521/orclpdb
```

---

### 🛠️ Key SQL*Plus Environment Commands

SQL\*Plus environment formatting commands do **not** require a trailing semicolon `;`.

| Command | Purpose / Function |
| :--- | :--- |
| **`SET SERVEROUTPUT ON`** | Enables display of PL/SQL output (`DBMS_OUTPUT.PUT_LINE`). |
| **`SET LINESIZE n`** | Sets output line width (e.g., `SET LINESIZE 150`). |
| **`SET PAGESIZE n`** | Sets number of lines per page before repeating headers (e.g., `SET PAGESIZE 50`). |
| **`SET FEEDBACK OFF`** | Suppresses query row count messages (e.g., *"10 rows selected"*). |
| **`DESCRIBE table_name`** | Displays table column structure, data types, and nullability. |

---

### 📜 Script Execution & Logging in SQL*Plus

#### 1. Execute an External `.sql` Script:
```text
SQL> @C:\scripts\create_tables.sql
-- OR --
SQL> START C:\scripts\create_tables.sql
```

#### 2. Log Query Output to a Text File (`SPOOL`):
```text
SQL> SPOOL C:\logs\output_report.txt
SQL> SELECT * FROM employees;
SQL> SPOOL OFF
```

---

## 🎯 STEP 15 — Practice Questions

1. **Question 1:** What is the purpose of Oracle's `DUAL` table? Write a query using `DUAL` to display the current logged-in database user.
2. **Question 2:** Explain the difference between `ROWNUM` and `ROWID` in Oracle Database.
3. **Question 3:** What SQL\*Plus command is required to enable output from `DBMS_OUTPUT.PUT_LINE` statements?
4. **Question 4:** Write an Oracle SQL 12c+ query to fetch rows `21` to `30` of employees sorted by `hire_date` ascending.

---

## ⏩ Navigation
* ⏪ **Previous Step:** **[Step 14 — TCL & Transactions](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_14_TCL_Commands.md)**
* ⏩ **Next Step:** **[Step 16 — PL/SQL Masterclass 🔥](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_16_PL_SQL.md)** — Learn procedural programming, cursors, procedures, triggers, and packages!

