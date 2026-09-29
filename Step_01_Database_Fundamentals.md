# 📘 STEP 1 — Database Fundamentals (0% → 5%)

---

## 🏆 SQL 0% → 100% Roadmap

```text
SQL
│
├── 0-5%     Database Fundamentals (STEP 1) 👈 (You are here)
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
└── 96-100%  PL/SQL (Variables, Loops, Procedures, Functions, Cursors, Triggers, Packages) 🔥 (STEP 16)
```

---

## 1️⃣ Core Concepts

### 1. Data
* **Definition:** Unprocessed, raw facts, numbers, text, or symbols without context.
* **Example:** `18`, `Darshan`, `Rajkot`

### 2. Information
* **Definition:** Data that has been processed, structured, or contextualized to be meaningful.
* **Example:** *"Darshan is 18 years old and lives in Rajkot."*

### 3. Database
* **Definition:** An organized collection of related data stored systematically in an electronic system so that it can be easily accessed, managed, updated, and queried.

### 4. DBMS (Database Management System)
* **Definition:** Software that interacts with end users, applications, and the database itself to capture, store, analyze, and retrieve data.
* **Examples:** MS Access, FileMaker.

### 5. RDBMS (Relational Database Management System)
* **Definition:** An advanced database system based on Edgar F. Codd's relational model, storing data in interconnected **Tables** (consisting of Rows and Columns) with predefined relationships between them.
* **Examples:** Oracle Database, MySQL, PostgreSQL, Microsoft SQL Server.

---

## 📊 RDBMS Table Architecture

Consider a `students` table in a `college` database:

#### `students` Table Example:

| id (Primary Key) | name | age | city |
| :--- | :--- | :--- | :--- |
| **101** | Darshan | 18 | Rajkot |
| **102** | Rahul | 20 | Ahmedabad |
| **103** | Priya | 19 | Surat |

---

### 6. Table (Relation)
* **Definition:** A structured grid composed of horizontal rows and vertical columns that holds related data within a database.

### 7. Row / Record / Tuple
* **Definition:** A single horizontal entry in a table representing a single, complete record of an entity (e.g., information about one student).
* **Synonyms:** Record, Tuple.
* **Example:** `101 | Darshan | 18 | Rajkot` is a single **Row**.

### 8. Column / Field / Attribute
* **Definition:** A vertical entity in a table representing a specific attribute or property of the stored entity across all records.
* **Synonyms:** Field, Attribute.
* **Example:** The `name` column contains only student names.

### 9. Primary Key
* **Definition:** A specific column (or combination of columns) that uniquely identifies each row/record in a table.
* **Rules:**
  1. Must contain **unique** values (no duplicates allowed).
  2. Cannot contain `NULL` (empty) values.
* **Example:** `id` in the `students` table.

### 10. Query
* **Definition:** A formal request or instruction sent to a database to retrieve, create, update, or remove data.
* **Example:** `SELECT name FROM students WHERE city = 'Rajkot';`

### 11. Constraint
* **Definition:** Rules enforced on table columns to restrict the types of data that can be inserted, ensuring accuracy and data integrity.
* **Example:** `age >= 18` or `NOT NULL`.

---

## 💡 Summary Comparison

| Concept | Row / Record / Tuple | Column / Field / Attribute |
| :--- | :--- | :--- |
| **Orientation** | Horizontal | Vertical |
| **Represents** | A single complete record/entity | A specific attribute or property |
| **Example** | Entire record for Darshan | `age` or `city` attribute |

---

## 🎯 STEP 1 — Practice Questions

1. **Question 1:** What is the fundamental difference between **Data** and **Information**?
2. **Question 2:** What are the two alternate terms used for a **Row** in RDBMS?
3. **Question 3:** What is a **Primary Key** and what are its two mandatory rules?
4. **Question 4:** Design a hypothetical **`courses`** table. List 4 attributes/columns for it and state which column should serve as the **Primary Key**.

---

## ⏩ Navigation
* ⏩ **Next Step:** **[Step 02 — SQL Introduction & CRUD](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_02_SQL_Introduction_and_CRUD.md)** — Start writing actual SQL statements!

