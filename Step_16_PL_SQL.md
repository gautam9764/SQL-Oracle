# 📘 STEP 16 — PL/SQL Masterclass 🔥 (96% → 100%)

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
├── 94-96%   Oracle SQL & SQL*Plus (STEP 15)
└── 96-100%  PL/SQL (Variables, Loops, Procedures, Functions, Cursors, Triggers, Packages) 🔥 👈 (You are here)
```

---

## 1️⃣ What is PL/SQL?

* **Full Form:** **Procedural Language / Structured Query Language**.
* **Definition:** PL/SQL is Oracle Corporation's procedural extension for SQL. It combines the data manipulation power of SQL with procedural programming structures such as conditional branching (`IF-THEN`), iterative loops (`FOR`/`WHILE`), variable declarations, exception handling, and modular packaging.
* **Architecture:** Executed directly inside the Oracle DB server's PL/SQL Engine, dramatically reducing network traffic between application servers and the database.

---

## 2️⃣ Basic PL/SQL Block Structure

A PL/SQL block is the fundamental building block of PL/SQL programming.

```sql
DECLARE
    -- [Optional] Variable, constant, cursor, and exception declarations
    v_message VARCHAR2(100) := 'Hello, PL/SQL World!';
BEGIN
    -- [Mandatory] Executable SQL & PL/SQL statements
    DBMS_OUTPUT.PUT_LINE(v_message);
EXCEPTION
    -- [Optional] Exception handling routines
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred.');
END;
/
```

---

## 3️⃣ Variables & Anchored Data Types (`%TYPE` & `%ROWTYPE`)

### 1. Standard Variable Declarations:
```sql
v_emp_id    NUMBER(6) := 101;
v_salary    DECIMAL(10, 2) DEFAULT 50000;
c_tax_rate  CONSTANT NUMBER(3, 2) := 0.18; -- Cannot be changed
```

### 2. `%TYPE` Attribute (Anchored Column Type):
Inherits the exact data type and precision of an existing table column automatically.
```sql
v_emp_name  employees.first_name%TYPE;
v_emp_sal   employees.salary%TYPE;
```

### 3. `%ROWTYPE` Attribute (Anchored Record Type):
Declares a composite record variable holding a complete row structure of a table.
```sql
v_emp_record  employees%ROWTYPE;
```

---

## 4️⃣ Control Structures

### 1️⃣ Conditional Statements (`IF-THEN-ELSIF`)
```sql
IF v_salary > 80000 THEN
    v_bonus := v_salary * 0.15;
ELSIF v_salary >= 50000 THEN
    v_bonus := v_salary * 0.10;
ELSE
    v_bonus := v_salary * 0.05;
END IF;
```

---

### 2️⃣ Iterative Control Loops

#### 1. Simple Loop (`EXIT WHEN`):
```sql
DECLARE
    v_counter NUMBER := 1;
BEGIN
    LOOP
        DBMS_OUTPUT.PUT_LINE('Counter: ' || v_counter);
        v_counter := v_counter + 1;
        EXIT WHEN v_counter > 5;
    END LOOP;
END;
/
```

#### 2. Numeric FOR Loop:
```sql
BEGIN
    FOR i IN 1..5 LOOP
        DBMS_OUTPUT.PUT_LINE('Iteration: ' || i);
    END LOOP;
END;
/
```

---

## 5️⃣ Cursors in PL/SQL ⭐

A **Cursor** is a pointer to a context area in memory allocated by the database to process multi-row SQL queries.

### 1. Implicit Cursors (`SQL%` Attributes):
Managed automatically by Oracle during `INSERT`, `UPDATE`, `DELETE`, and single-row `SELECT INTO`.
* `SQL%FOUND` → Returns `TRUE` if DML affected 1+ rows.
* `SQL%NOTFOUND` → Returns `TRUE` if DML affected 0 rows.
* `SQL%ROWCOUNT` → Returns total number of rows affected.

---

### 2. Explicit Cursors (4-Step Lifecycle)
Used to fetch and process multi-row result sets row-by-row manually.

```sql
DECLARE
    -- Step 1: Declare the cursor
    CURSOR emp_cursor IS
        SELECT employee_id, first_name, salary 
        FROM employees 
        WHERE department_id = 20;

    v_id   employees.employee_id%TYPE;
    v_name employees.first_name%TYPE;
    v_sal  employees.salary%TYPE;
BEGIN
    -- Step 2: Open the cursor
    OPEN emp_cursor;

    LOOP
        -- Step 3: Fetch next row into variables
        FETCH emp_cursor INTO v_id, v_name, v_sal;
        EXIT WHEN emp_cursor%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE('Emp ID: ' || v_id || ' | Name: ' || v_name || ' | Sal: ' || v_sal);
    END LOOP;

    -- Step 4: Close the cursor
    CLOSE emp_cursor;
END;
/
```

#### 💡 Modern Cursor FOR Loop (Automatic Open, Fetch, Close):
```sql
BEGIN
    FOR rec IN (SELECT employee_id, first_name, salary FROM employees WHERE department_id = 20) LOOP
        DBMS_OUTPUT.PUT_LINE(rec.first_name || ' earns ' || rec.salary);
    END LOOP;
END;
/
```

---

## 6️⃣ Exception Handling

Catches and handles runtime errors gracefully.

### Predefined Exceptions:
* `NO_DATA_FOUND` → Query returned zero rows.
* `TOO_MANY_ROWS` → Single-row `SELECT INTO` returned multiple rows.
* `ZERO_DIVIDE` → Division by zero attempted.
* `DUP_VAL_ON_INDEX` → Attempted to insert duplicate value into unique key.

```sql
DECLARE
    v_name employees.first_name%TYPE;
BEGIN
    SELECT first_name INTO v_name FROM employees WHERE employee_id = 9999;
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Error: Employee record does not exist.');
    WHEN OTHERS THEN
        RAISE_APPLICATION_ERROR(-20001, 'An unhandled exception occurred.');
END;
/
```

---

## 7️⃣ Stored Procedures & Functions

### 1. Stored Procedure:
Performs actions or business logic operations. Can return zero, one, or multiple values via `OUT` parameters.

```sql
CREATE OR REPLACE PROCEDURE update_emp_salary (
    p_emp_id IN NUMBER,
    p_increase_pct IN NUMBER
) AS
BEGIN
    UPDATE employees
    SET salary = salary + (salary * (p_increase_pct / 100))
    WHERE employee_id = p_emp_id;

    COMMIT;
END update_emp_salary;
/
```

---

### 2. Stored Function:
Calculates and **MUST return a single value** using the `RETURN` keyword. Can be invoked inside standard SQL `SELECT` queries.

```sql
CREATE OR REPLACE FUNCTION get_annual_income (
    p_salary IN NUMBER,
    p_comm IN NUMBER
) RETURN NUMBER IS
BEGIN
    RETURN (p_salary * 12) + NVL(p_comm, 0);
END get_annual_income;
/

-- Calling function in SQL:
SELECT first_name, get_annual_income(salary, commission_pct) AS annual_pay 
FROM employees;
```

---

## 8️⃣ Database Triggers ⭐

A **Trigger** is a named PL/SQL block stored in the database that automatically executes (fires) in response to specific DML events (`INSERT`, `UPDATE`, `DELETE`) on a table.

### Audit Trigger Example (`BEFORE` / `AFTER` Row-Level):
Uses `:OLD` and `:NEW` pseudo-record references.

```sql
CREATE OR REPLACE TRIGGER trg_audit_emp_salary
BEFORE UPDATE OF salary ON employees
FOR EACH ROW
BEGIN
    IF :NEW.salary < :OLD.salary THEN
        RAISE_APPLICATION_ERROR(-20002, 'Salary reduction is prohibited.');
    END IF;
END;
/
```

---

## 9️⃣ PL/SQL Packages

A **Package** is an enterprise container that groups logically related procedures, functions, variables, cursors, and type definitions together.

### 1. Package Specification (Header / Public Interface):
```sql
CREATE OR REPLACE PACKAGE emp_pkg AS
    PROCEDure add_employee(p_id NUMBER, p_name VARCHAR2, p_sal NUMBER);
    FUNCTION get_emp_salary(p_id NUMBER) RETURN NUMBER;
END emp_pkg;
/
```

### 2. Package Body (Implementation Details):
```sql
CREATE OR REPLACE PACKAGE BODY emp_pkg AS

    PROCEDURE add_employee(p_id NUMBER, p_name VARCHAR2, p_sal NUMBER) IS
    BEGIN
        INSERT INTO employees (employee_id, first_name, salary)
        VALUES (p_id, p_name, p_sal);
    END add_employee;

    FUNCTION get_emp_salary(p_id NUMBER) RETURN NUMBER IS
        v_sal NUMBER;
    BEGIN
        SELECT salary INTO v_sal FROM employees WHERE employee_id = p_id;
        RETURN v_sal;
    END get_emp_salary;

END emp_pkg;
/
```

---

## 🎯 STEP 16 — Practice Questions

1. **Question 1:** What is the difference between `%TYPE` and `%ROWTYPE` in PL/SQL variable declarations?
2. **Question 2:** Explain the 4 steps of an Explicit Cursor lifecycle (`DECLARE`, `OPEN`, `FETCH`, `CLOSE`).
3. **Question 3:** What is the primary difference between a **Stored Procedure** and a **Stored Function**?
4. **Question 4:** What are the `:OLD` and `:NEW` references inside an `UPDATE` row-level trigger?

---

## ⏩ Navigation
* ⏪ **Previous Step:** **[Step 15 — Oracle SQL & SQL*Plus](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_15_Oracle_SQL_and_SQLPlus.md)**
* 🏠 **Main Index:** **[Master Roadmap Index (README.md)](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/README.md)**

