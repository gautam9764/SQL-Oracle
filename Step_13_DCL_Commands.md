# 📘 STEP 13 — DCL Commands (88% → 91%)

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
├── 88-91%   DCL Commands (GRANT, REVOKE) (STEP 13) 👈 (You are here)
├── 91-94%   TCL & Transactions (COMMIT, ROLLBACK, SAVEPOINT) (STEP 14)
├── 94-96%   Oracle SQL & SQL*Plus (STEP 15)
└── 96-100%  PL/SQL (Variables, Loops, Procedures, Functions, Cursors, Triggers, Packages) 🔥 (STEP 16)
```

---

## 1️⃣ What is DCL (Data Control Language)?

* **Definition:** Data Control Language (DCL) consists of SQL commands used to manage security, user authorization, and access control permissions over database objects.
* **Core Purpose:** Protects database integrity by ensuring users can only view or modify database objects for which they have explicit permissions.
* **2 Primary DCL Commands:**
  * `GRANT` → Gives specific access permissions or privileges to users or roles.
  * `REVOKE` → Withdraws or cancels previously granted privileges.

---

## 2️⃣ Types of Database Privileges

In RDBMS security model, privileges are divided into two main categories:

```text
Database Privileges
├── 1. System Privileges  (Administrative rights over database system: CREATE TABLE, CREATE USER, etc.)
└── 2. Object Privileges  (Rights over specific database objects: SELECT, INSERT, UPDATE on a table)
```

### 1. System Privileges
Administrative rights allowing a user to perform system-wide actions:
* `CREATE SESSION` → Log in to the database.
* `CREATE TABLE` → Create tables in user's schema.
* `CREATE USER` / `DROP USER` → Manage database accounts.
* `CREATE VIEW`, `CREATE PROCEDURE`, `CREATE SEQUENCE`.

### 2. Object Privileges
Permissions to perform specific DML/DQL actions on specific objects (tables, views, stored procedures):
* `SELECT` → Read data from a table/view.
* `INSERT` → Insert new rows into a table.
* `UPDATE` → Modify rows in a table.
* `DELETE` → Remove rows from a table.
* `EXECUTE` → Run a PL/SQL stored procedure or function.
* `ALL PRIVILEGES` → Grants all object permissions on a specified table.

---

## 3️⃣ The `GRANT` Statement

The `GRANT` command assigns privileges to a user, role, or `PUBLIC` (all users).

### 1. Granting Object Privileges
```sql
-- Granting SELECT and INSERT privileges on employees table to user 'john_doe'
GRANT SELECT, INSERT ON employees TO john_doe;

-- Granting ALL privileges on products table to user 'admin_user'
GRANT ALL PRIVILEGES ON products TO admin_user;
```

### 2. Granting System Privileges
```sql
GRANT CREATE SESSION, CREATE TABLE TO analyst_user;
```

### 3. `WITH GRANT OPTION`
Allows the grantee user to pass the permission along to other users:
```sql
GRANT SELECT ON employees TO manager_user WITH GRANT OPTION;
```

---

## 4️⃣ The `REVOKE` Statement

The `REVOKE` command cancels previously assigned privileges.

### Syntax & Examples:
```sql
-- Revoking INSERT and UPDATE permissions on employees table from user 'john_doe'
REVOKE INSERT, UPDATE ON employees FROM john_doe;

-- Revoking System Privileges
REVOKE CREATE TABLE FROM analyst_user;

-- Revoking ALL privileges
REVOKE ALL PRIVILEGES ON products FROM admin_user;
```

---

## 5️⃣ Role-Based Access Control (RBAC)

Granting privileges user by user is inefficient and error-prone in enterprise applications. Instead, databases use **Roles** to group permissions.

```text
[ Privileges ] ──GRANT TO──> [ Role ] ──GRANT TO──> [ Users ]
```

### Example RBAC Workflow:
```sql
-- 1. Create a database role
CREATE ROLE hr_analyst;

-- 2. Grant object privileges to the role
GRANT SELECT, UPDATE ON employees TO hr_analyst;
GRANT SELECT ON departments TO hr_analyst;

-- 3. Assign the role to specific users
GRANT hr_analyst TO user_alex, user_sarah;

-- 4. Revoke the role when a user changes positions
REVOKE hr_analyst FROM user_alex;
```

---

## 💡 DCL Summary Table

| Command | Action | Key Options | Example |
| :--- | :--- | :--- | :--- |
| **`GRANT`** | Gives permissions to user/role | `WITH GRANT OPTION`, `PUBLIC` | `GRANT SELECT ON emp TO user1;` |
| **`REVOKE`** | Removes permissions from user/role | N/A | `REVOKE SELECT ON emp FROM user1;` |
| **`CREATE ROLE`** | Defines a privilege container | N/A | `CREATE ROLE read_only_role;` |

---

## 🎯 STEP 13 — Practice Questions

1. **Question 1:** What is the fundamental difference between **System Privileges** and **Object Privileges**?
2. **Question 2:** What does the `WITH GRANT OPTION` clause do when attached to a `GRANT` statement?
3. **Question 3:** Why is Role-Based Access Control (RBAC) preferred over granting privileges directly to individual users?
4. **Question 4:** Write an SQL DCL query to revoke `DELETE` permissions on the `orders` table from the user `intern_account`.

---

## ⏩ Navigation
* ⏪ **Previous Step:** **[Step 12 — Views, Indexes, Sequences & Synonyms](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_12_Views_Index_Sequence_Synonym.md)**
* ⏩ **Next Step:** **[Step 14 — TCL & Transactions](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_14_TCL_Commands.md)** — Learn transactions, `COMMIT`, `ROLLBACK`, `SAVEPOINT`, and ACID properties!

