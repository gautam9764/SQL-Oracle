# 📘 STEP 2 — SQL Introduction & CRUD (5% → 10%)

---

## 🏆 SQL 0% → 100% Roadmap

```text
SQL
│
├── 0-5%     Database Fundamentals (STEP 1)
├── 5-10%    SQL Introduction & CRUD (STEP 2) 👈 (You are here)
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

## 1️⃣ What is SQL?

* **Full Form:** **Structured Query Language**.
* **Pronunciation:** "S-Q-L" or "Sequel".
* **Definition:** SQL is the standard domain-specific language used to store, manipulate, manage, and retrieve data in Relational Database Management Systems (RDBMS) such as Oracle, MySQL, PostgreSQL, and MS SQL Server.
* **Core Purpose:** Enables developers and data professionals to query databases, insert new records, update existing records, delete unwanted records, and manage database structures (tables, views, indexes).

---

## 2️⃣ SQL vs MySQL vs Oracle vs DBMS

Understanding the distinction between these terms is fundamental:

| Concept | What is it? | Role / Category | Example |
| :--- | :--- | :--- | :--- |
| **SQL** | **Language** | The standard language used to interact with RDBMS. | SQL Queries (`SELECT * FROM table;`) |
| **DBMS** | **Category / Concept** | Any software system used to create and manage databases. | General database management concept |
| **MySQL** | **Software (RDBMS Engine)** | An open-source relational database management system. | MySQL 8.0 Engine |
| **Oracle** | **Software (RDBMS Engine)** | An enterprise-grade, advanced relational database management system. | Oracle Database 19c/21c |

> [!NOTE]
> **Analogy:** 
> * **SQL** is like a **language** (e.g., English).
> * **MySQL & Oracle** are like **people or systems** that understand and speak that language.

---

## 3️⃣ SQL Keywords

* **Definition:** Reserved words in SQL that have special meaning to the database engine and are used to execute specific commands.
* **Essential Keywords:**
  * `SELECT` → Retrieves data from one or more tables.
  * `INSERT` → Adds new rows of data to a table.
  * `UPDATE` → Modifies existing data in a table.
  * `DELETE` → Removes rows of data from a table.
  * `CREATE` → Creates a new database object (table, view, index).
  * `DROP` → Deletes an entire database object.
  * `FROM` → Specifies the table to retrieve data from.
  * `WHERE` → Filters records based on specific conditions.

---

## 4️⃣ SQL Syntax Rules

1. **Case Sensitivity:** SQL keywords are **case-insensitive** (`SELECT` is identical to `select`). However, it is an industry **best practice** to write SQL keywords in `UPPERCASE` and table/column names in `lowercase` or `snake_case`.
2. **Semicolon `;`:** A semicolon marks the termination of an SQL statement in standard database environments.
3. **Comments in SQL:**
   * **Single-line comment:** `-- This is a single-line comment`
   * **Multi-line comment:** `/* This is a multi-line comment */`

---

## 5️⃣ SQL Statements

* An **SQL Statement** is a valid command sent to the RDBMS to perform a specific action.
* **Example:**
  ```sql
  SELECT name, age FROM students WHERE city = 'New York';
  ```

---

## 6️⃣ CRUD Operations ⭐

In any Relational Database, all fundamental data operations fall into **4 categories** known as **CRUD**:

```text
C → Create  (Adding new data)
R → Read    (Fetching / Querying existing data)
U → Update  (Modifying existing data)
D → Delete  (Removing unwanted data)
```

### 🔄 CRUD Mapping to SQL Commands:

| CRUD Operation | Description | SQL Command | Example Syntax |
| :--- | :--- | :--- | :--- |
| **C - Create** | Insert new records | `INSERT INTO` | `INSERT INTO students (id, name) VALUES (101, 'Darshan');` |
| **R - Read** | Fetch / view records | `SELECT` | `SELECT * FROM students;` |
| **U - Update** | Modify existing records | `UPDATE ... SET` | `UPDATE students SET age = 20 WHERE id = 101;` |
| **D - Delete** | Remove records | `DELETE FROM` | `DELETE FROM students WHERE id = 101;` |

---

## 🎯 STEP 2 — Practice Questions

1. **Question 1:** What is the primary difference between **SQL** and **MySQL**?
2. **Question 2:** What does **CRUD** stand for, and which SQL command performs the **Read** operation?
3. **Question 3:** What is the syntax for single-line and multi-line comments in SQL?
4. **Question 4:** Which SQL keyword is used to modify existing records in a table?
   - A) `CHANGE`
   - B) `MODIFY`
   - C) `UPDATE`
   - D) `ALTER`

---

## ⏩ Navigation
* ⏪ **Previous Step:** **[Step 01 — Database Fundamentals](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_01_Database_Fundamentals.md)**
* ⏩ **Next Step:** **[Step 03 — Data Types](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_03_Data_Types.md)** — Learn how data is categorized and stored in columns!

