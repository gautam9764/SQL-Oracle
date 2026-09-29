# 📘 STEP 14 — TCL & Transactions (91% → 94%)

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
├── 91-94%   TCL & Transactions (COMMIT, ROLLBACK, SAVEPOINT) (STEP 14) 👈 (You are here)
├── 94-96%   Oracle SQL & SQL*Plus (STEP 15)
└── 96-100%  PL/SQL (Variables, Loops, Procedures, Functions, Cursors, Triggers, Packages) 🔥 (STEP 16)
```

---

## 1️⃣ What is a Transaction?

* **Definition:** A **Transaction** is a logical unit of work consisting of one or more SQL statements (typically DML operations like `INSERT`, `UPDATE`, `DELETE`) executed as a single, indivisible sequence.
* **All-or-Nothing Rule:** A transaction must either succeed completely (all changes saved to database) or fail completely (all changes reverted as if nothing happened).

---

## 2️⃣ The ACID Properties ⭐

Every transaction in a Relational Database must strictly adhere to the **4 ACID Properties** to guarantee data reliability and integrity:

```text
A → Atomicity    ("All or Nothing")
C → Consistency  ("Valid state to valid state")
I → Isolation    ("Transactions run independently")
D → Durability   ("Committed data is permanent")
```

| Property | Full Name | Explanation |
| :--- | :--- | :--- |
| **A** | **Atomicity** | Ensures that all statements within a transaction complete successfully. If any single statement fails, the entire transaction is aborted and rolled back. |
| **C** | **Consistency** | Ensures that data moves from one valid database state to another, strictly obeying all constraints, foreign keys, and rules. |
| **I** | **Isolation** | Ensures that concurrent transactions execute independently of one another without visible intermediate side-effects. |
| **D** | **Durability** | Guarantees that once a transaction is committed, its changes are permanently stored on non-volatile disk storage, surviving power failures or crashes. |

---

## 3️⃣ Core TCL Commands

Transaction Control Language (TCL) commands manage the lifecycle of database transactions:

### 1. `COMMIT`
Permanently saves all pending DML changes executed during the current transaction to disk and releases row locks.

```sql
UPDATE accounts SET balance = balance - 500 WHERE account_id = 101;
UPDATE accounts SET balance = balance + 500 WHERE account_id = 102;
COMMIT; -- All changes are now permanent
```

### 2. `ROLLBACK`
Undoes all uncommitted DML changes made since the beginning of the transaction or back to a specific `SAVEPOINT`.

```sql
DELETE FROM accounts WHERE account_id = 101;
ROLLBACK; -- Undoes the deletion, account 101 is restored!
```

### 3. `SAVEPOINT`
Creates a named intermediate checkpoint within a transaction, allowing partial rollbacks without cancelling the entire transaction.

```sql
SAVEPOINT sp1;
```

---

## 4️⃣ Real-World Walkthrough: Bank Funds Transfer ⭐

Consider transferring $500 from Alice (Account `101`) to Bob (Account `102`):

```sql
-- Step 1: Start Transaction (Explicit or Implicit)
UPDATE accounts 
SET balance = balance - 500 
WHERE account_id = 101;

-- Step 2: Create a savepoint after the debit operation
SAVEPOINT after_debit;

-- Step 3: Attempt to credit Bob's account
UPDATE accounts 
SET balance = balance + 500 
WHERE account_id = 102;

-- Step 4A: If Bob's account update succeeded -> Permanent Commit
COMMIT;

-- Step 4B: If Bob's account update failed -> Partial Rollback to Savepoint
-- ROLLBACK TO after_debit;
```

---

## 💡 Implicit vs Explicit Commits

1. **Explicit Commit:** Handled manually by executing `COMMIT;` or `ROLLBACK;`.
2. **Implicit Commit:** Occurs automatically when:
   * Any **DDL command** (`CREATE`, `ALTER`, `DROP`, `TRUNCATE`) is executed.
   * Any **DCL command** (`GRANT`, `REVOKE`) is executed.
   * Normal disconnection from database tool (e.g., exiting SQL*Plus).

---

## 🎯 STEP 14 — Practice Questions

1. **Question 1:** What does the **Atomicity** property of ACID guarantee during a database transaction?
2. **Question 2:** What is the purpose of creating a `SAVEPOINT` inside a transaction?
3. **Question 3:** What happens if a DDL command like `CREATE TABLE` is executed in the middle of an uncommitted DML transaction?
4. **Question 4:** Write a transaction block using SQL that updates an order status to `'SHIPPED'`, creates a savepoint named `sp_ship`, updates inventory counts, and rolls back to `sp_ship` if an error occurs.

---

## ⏩ Navigation
* ⏪ **Previous Step:** **[Step 13 — DCL Commands](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_13_DCL_Commands.md)**
* ⏩ **Next Step:** **[Step 15 — Oracle SQL & SQL*Plus](file:///f:/document/Databases/SQL/sql%200%20to%20100%25/Step_15_Oracle_SQL_and_SQLPlus.md)** — Explore `DUAL` table, `ROWNUM`, `ROWID`, and SQL*Plus client commands!

