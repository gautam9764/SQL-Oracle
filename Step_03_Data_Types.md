# 📘 STEP 3 — Data Types (10% → 15%)

---

## 🏆 SQL 0% → 100% Roadmap

```text
SQL
│
├── 0-5%     Database Fundamentals (STEP 1)
├── 5-10%    SQL Introduction & CRUD (STEP 2)
├── 10-15%   Data Types (STEP 3) 👈 (You are here)
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
└── 96-100%  PL/SQL (Variables, Loops, Procedures, Functions, Cursors, Triggers, Packages) 🔥 (STEP 16)
```

---

## 1️⃣ What is an SQL Data Type?

* **Definition:** A data type specifies the type of value a table column can hold, such as integer numbers, decimal numbers, text strings, dates, or binary objects.
* **Importance:**
  1. Enforces data integrity by preventing invalid entries (e.g., entering letters into an `AGE` column).
  2. Optimizes storage allocation in memory and disk space.
  3. Dictates which operations and functions can be applied to the column.

---

## 2️⃣ Core Data Type Categories

SQL Data Types are broadly categorized into **5 major groups**:

```text
SQL Data Types
├── 1. Numeric Types       (INT, NUMBER, DECIMAL, FLOAT)
├── 2. String/Character    (CHAR, VARCHAR / VARCHAR2, TEXT)
├── 3. Date & Time Types   (DATE, TIMESTAMP, TIME)
├── 4. Large Objects (LOB) (CLOB, BLOB)
└── 5. Boolean & Misc      (BOOLEAN, JSON, XML)
```

---

## 3️⃣ Detailed Breakdown of Data Types

### 🔢 1. Numeric Data Types

Used to store integer and floating-point values (ages, salaries, quantities, ratings).

| Data Type | Description | Oracle Equivalent | MySQL Equivalent | Example |
| :--- | :--- | :--- | :--- | :--- |
| **`INT` / `INTEGER`** | Standard whole numbers (no decimal). | `NUMBER(38)` | `INT` / `INTEGER` | `25`, `1004` |
| **`SMALLINT`** | Small range whole numbers. | `NUMBER(5)` | `SMALLINT` | `32000` |
| **`BIGINT`** | Extremely large whole numbers. | `NUMBER(19)` | `BIGINT` | `9223372036854775807` |
| **`DECIMAL(p, s)`** | Fixed-point numbers with exact precision `p` and scale `s`. | `NUMBER(p, s)` | `DECIMAL(p, s)` | `DECIMAL(10,2)` → `12345678.90` |
| **`FLOAT` / `DOUBLE`** | Floating-point numbers with variable precision. | `FLOAT` / `BINARY_FLOAT` | `FLOAT` / `DOUBLE` | `3.14159` |

> [!TIP]
> **Precision (`p`) vs Scale (`s`) in `DECIMAL(p, s)` or `NUMBER(p, s)`:**
> * **`p` (Precision):** Total number of digits (both left and right of the decimal point).
> * **`s` (Scale):** Number of digits to the right of the decimal point.
> * *Example:* `DECIMAL(6, 2)` can hold up to `9999.99`.

---

### 🔤 2. Character & String Data Types

Used to store names, addresses, descriptions, codes, and general text.

| Data Type | Type | Max Size | Key Characteristics | Best Use Case |
| :--- | :--- | :--- | :--- | :--- |
| **`CHAR(n)`** | Fixed-length string | Up to 2,000 bytes | Right-pads with spaces if the string is shorter than `n`. | Fixed length codes like `country_code CHAR(2)` ('US', 'IN') |
| **`VARCHAR(n)`** | Variable-length string | Up to 65,535 bytes (MySQL) | Allocates memory dynamically based on string length. | Standard text fields like `email VARCHAR(100)` |
| **`VARCHAR2(n)`** | Variable-length string | Up to 4,000 bytes (Oracle) | Oracle-specific recommended variable text type. | Oracle DB names, addresses |
| **`TEXT`** | Large text field | Up to 65,535 chars | Variable-length long text. | Blog post contents, comments |

---

### 📅 3. Date & Time Data Types

Used to store temporal values like hire dates, order timestamps, and transaction times.

| Data Type | Format | Includes Timezone? | Example |
| :--- | :--- | :--- | :--- |
| **`DATE`** | `YYYY-MM-DD` (MySQL) / `DD-MON-YY` (Oracle) | No | `'2026-08-28'` |
| **`TIME`** | `HH:MI:SS` | No | `'14:30:00'` |
| **`DATETIME`** | `YYYY-MM-DD HH:MI:SS` | No | `'2026-08-28 14:30:00'` |
| **`TIMESTAMP`** | `YYYY-MM-DD HH:MI:SS.FF` | Optional | `'2026-08-28 14:30:00.123456'` |

---

### 📦 4. Large Object (LOB) Data Types

Used to store massive unstructured data like multimedia, PDFs, or large JSON documents.

| LOB Type | Name | Purpose | Example |
| :--- | :--- | :--- | :--- |
| **`CLOB`** | Character Large Object | Stores massive text documents (up to 4 GB). | XML/JSON files, book manuscripts |
| **`BLOB`** | Binary Large Object | Stores binary files (up to 4 GB). | Images, audio, video files, PDFs |

---

## 4️⃣ Type Conversion (Casting)

Converting data from one type to another explicitly:

### 1. `CAST()` Function (ANSI Standard SQL)
```sql
SELECT CAST('123' AS INT) AS converted_number;
SELECT CAST(123.456 AS DECIMAL(5, 2)) AS rounded_val;
```

### 2. Oracle-Specific Conversion Functions
* **`TO_NUMBER('123')`** → Converts string to number.
* **`TO_CHAR(sysdate, 'YYYY-MM-DD')`** → Converts date/number to string.
* **`TO_DATE('2026-08-28', 'YYYY-MM-DD')`** → Converts formatted string to date.

---

## 🎯 STEP 3 — Practice Questions

1. **Question 1:** What is the difference between `CHAR(10)` and `VARCHAR2(10)` in terms of memory storage?
2. **Question 2:** If a column is defined as `DECIMAL(7, 3)`, what is the largest number it can store?
3. **Question 3:** Which LOB data type is used to store images and PDF files directly inside a database table?
4. **Question 4:** What is the output of `CAST(45.678 AS INT)` in ANSI SQL?

---

## ⏩ Navigation
* ⏪ **Previous Step:** **[Step 02 — SQL Introduction & CRUD](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_02_SQL_Introduction_and_CRUD.md)**
* ⏩ **Next Step:** **[Step 04 — DDL Commands](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_04_DDL_Commands.md)** — Learn how to create and alter table structures using data types!

