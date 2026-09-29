# SQL Commands Reference Guide

An all-in-one reference for SQL Commands categorized into **DDL**, **DML**, **TCL**, **DQL**, and **DCL**.

---

## SQL Commands Overview

```
                          SQL Commands
   ____________________________|____________________________
  |            |            |            |                  |
 DDL          DML          TCL          DQL                DCL
  |            |            |            |                  |
  |--CREATE    |--INSERT    |--BEGIN     |--SELECT          |--GRANT
  |--DROP      |--UPDATE    |  TRANS.    |--FROM            |--REVOKE
  |--ALTER     |--DELETE    |--COMMIT    |--WHERE           
  |--TRUNCATE               |--SAVEPOINT |--GROUP BY        
  |--COMMENT                |--ROLLBACK  |--HAVING          
  |--RENAME                              |--DISTINCT        
                                         |--ORDER BY        
                                         |--LIMIT           
```

---

## 1. Data Definition Language (DDL)

DDL commands are used to define, modify, and manage the structure of database objects such as tables, indexes, and views.

| Command | Description | Syntax |
| :--- | :--- | :--- |
| **CREATE** | Create database or its objects (table, index, function, views, store procedure and triggers) | `CREATE TABLE table_name (column1 data_type, column2 data_type, ...);` |
| **DROP** | Delete objects from the database | `DROP TABLE table_name;` |
| **ALTER** | Alter the structure of the database | `ALTER TABLE table_name ADD COLUMN column_name data_type;` |
| **TRUNCATE** | Remove all records from a table, including all spaces allocated for the records are removed | `TRUNCATE TABLE table_name;` |
| **COMMENT** | Add comments to the data dictionary | `COMMENT ON TABLE table_name IS 'comment_text';` |
| **RENAME** | Rename an object existing in the database | `RENAME TABLE old_table_name TO new_table_name;` |

---

## 2. Data Manipulation Language (DML)

DML commands are used to insert, update, and delete data within database tables.

| Command | Description | Syntax |
| :--- | :--- | :--- |
| **INSERT** | Insert data into a table | `INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);` |
| **UPDATE** | Update existing data within a table | `UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;` |
| **DELETE** | Delete records from a database table | `DELETE FROM table_name WHERE condition;` |

---

## 3. Transaction Control Language (TCL)

TCL commands manage transactions within the database to ensure data integrity.

| Command | Description | Syntax |
| :--- | :--- | :--- |
| **BEGIN TRANSACTION** | Starts a new transaction | `BEGIN TRANSACTION [transaction_name];` |
| **COMMIT** | Saves all changes made during the transaction | `COMMIT;` |
| **ROLLBACK** | Undoes all changes made during the transaction | `ROLLBACK;` |
| **SAVEPOINT** | Creates a savepoint within the current transaction | `SAVEPOINT savepoint_name;` |

---

## 4. Data Query Language (DQL)

DQL commands are used to query and retrieve data from database tables.

| Command | Description | Syntax |
| :--- | :--- | :--- |
| **SELECT** | It is used to retrieve data from the database | `SELECT column1, column2, ... FROM table_name WHERE condition;` |
| **FROM** | Indicates the table(s) from which to retrieve data | `SELECT column1 FROM table_name;` |
| **WHERE** | Filters rows before any grouping or aggregation | `SELECT column1 FROM table_name WHERE condition;` |
| **GROUP BY** | Groups rows that have the same values in specified columns | `SELECT column1, AVG(column2) FROM table_name GROUP BY column1;` |
| **HAVING** | Filters the results of GROUP BY | `SELECT column1, AVG(column2) FROM table_name GROUP BY column1 HAVING condition;` |
| **DISTINCT** | Removes duplicate rows from the result set | `SELECT DISTINCT column1, column2, ... FROM table_name;` |
| **ORDER BY** | Sorts the result set by one or more columns | `SELECT column1 FROM table_name ORDER BY column1 [ASC \| DESC];` |
| **LIMIT** | Used to restrict the number of rows returned in a SELECT query (commonly supported in MySQL and PostgreSQL) | `SELECT * FROM table_name LIMIT number;` |

---

## 5. Data Control Language (DCL)

DCL commands deal with rights, permissions, and security controls of the database system.

| Command | Description | Syntax |
| :--- | :--- | :--- |
| **GRANT** | Gives user access privileges to the database | `GRANT privilege_name ON object_name TO user_name;` |
| **REVOKE** | Withdraws user access privileges given by using the GRANT command | `REVOKE privilege_name ON object_name FROM user_name;` |
