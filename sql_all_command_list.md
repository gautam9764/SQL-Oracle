# SQL Commands Reference Guide

An all-in-one reference guide for SQL Commands categorized into **DDL**, **DML**, **TCL**, **DQL**, and **DCL** with descriptions, syntax, and practical examples.

---

## SQL Commands Hierarchy

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

## Quick Reference Summary Table

| Category | Command | Description | Syntax |
| :--- | :--- | :--- | :--- |
| **DDL** | **CREATE** | Create database objects (table, view, index, procedure) | `CREATE TABLE table_name (column1 data_type, ...);` |
| **DDL** | **DROP** | Delete objects permanently from database | `DROP TABLE table_name;` |
| **DDL** | **ALTER** | Modify structure of database object | `ALTER TABLE table_name ADD COLUMN column_name data_type;` |
| **DDL** | **TRUNCATE** | Remove all records from a table, freeing space | `TRUNCATE TABLE table_name;` |
| **DDL** | **COMMENT** | Add comments to the data dictionary | `COMMENT ON TABLE table_name IS 'comment_text';` |
| **DDL** | **RENAME** | Rename an existing database object | `RENAME TABLE old_name TO new_name;` |
| **DML** | **INSERT** | Insert new rows into a table | `INSERT INTO table_name (col1, col2) VALUES (val1, val2);` |
| **DML** | **UPDATE** | Update existing data in a table | `UPDATE table_name SET col1 = val1 WHERE condition;` |
| **DML** | **DELETE** | Remove records from a table based on condition | `DELETE FROM table_name WHERE condition;` |
| **TCL** | **BEGIN TRANSACTION** | Start a new transaction block | `BEGIN TRANSACTION;` |
| **TCL** | **COMMIT** | Save all changes made during current transaction | `COMMIT;` |
| **TCL** | **ROLLBACK** | Undo all changes made during current transaction | `ROLLBACK;` |
| **TCL** | **SAVEPOINT** | Create a checkpoint inside current transaction | `SAVEPOINT savepoint_name;` |
| **DQL** | **SELECT** | Retrieve data from database tables | `SELECT col1, col2 FROM table_name WHERE condition;` |
| **DQL** | **FROM** | Specify table(s) to retrieve data from | `SELECT * FROM table_name;` |
| **DQL** | **WHERE** | Filter rows before grouping or aggregation | `SELECT * FROM table_name WHERE condition;` |
| **DQL** | **GROUP BY** | Group rows sharing identical values | `SELECT col1, COUNT(*) FROM table_name GROUP BY col1;` |
| **DQL** | **HAVING** | Filter results of GROUP BY aggregation | `SELECT col1, AVG(col2) FROM table_name GROUP BY col1 HAVING AVG(col2) > 100;` |
| **DQL** | **DISTINCT** | Remove duplicate rows from result set | `SELECT DISTINCT col1 FROM table_name;` |
| **DQL** | **ORDER BY** | Sort result set by specified column(s) | `SELECT * FROM table_name ORDER BY col1 [ASC\|DESC];` |
| **DQL** | **LIMIT** | Restrict total number of rows returned | `SELECT * FROM table_name LIMIT number;` |
| **DCL** | **GRANT** | Give user access privileges | `GRANT privilege_name ON object_name TO user_name;` |
| **DCL** | **REVOKE** | Withdraw user access privileges | `REVOKE privilege_name ON object_name FROM user_name;` |

---

## Detailed SQL Commands Breakdown with Examples

---

### 1. Data Definition Language (DDL)

DDL commands are used to define, modify, and manage the structure of database objects (tables, indexes, views, and schemas).

#### 1.1 CREATE
* **Description**: Creates new database objects like tables, views, indexes, or procedures.
* **Syntax**:
  ```sql
  CREATE TABLE table_name (
      column1 data_type constraints,
      column2 data_type constraints,
      ...
  );
  ```
* **Example**:
  ```sql
  CREATE TABLE Employees (
      EmpID INT PRIMARY KEY,
      FirstName VARCHAR(50) NOT NULL,
      LastName VARCHAR(50),
      Salary DECIMAL(10, 2),
      HireDate DATE
  );
  ```

#### 1.2 DROP
* **Description**: Deletes an existing database object completely along with its structure and contents.
* **Syntax**:
  ```sql
  DROP TABLE table_name;
  ```
* **Example**:
  ```sql
  DROP TABLE Employees;
  ```

#### 1.3 ALTER
* **Description**: Modifies the structure of an existing table (add, delete, or modify columns/constraints).
* **Syntax**:
  ```sql
  -- Add column
  ALTER TABLE table_name ADD column_name data_type;

  -- Drop column
  ALTER TABLE table_name DROP COLUMN column_name;
  ```
* **Example**:
  ```sql
  ALTER TABLE Employees ADD Department VARCHAR(50);
  ALTER TABLE Employees DROP COLUMN LastName;
  ```

#### 1.4 TRUNCATE
* **Description**: Removes all rows from a table while keeping the table structure intact for future use. It also deallocates table storage space.
* **Syntax**:
  ```sql
  TRUNCATE TABLE table_name;
  ```
* **Example**:
  ```sql
  TRUNCATE TABLE Employees;
  ```

#### 1.5 COMMENT
* **Description**: Adds descriptive documentation/comments to table or column definitions in the data dictionary.
* **Syntax**:
  ```sql
  COMMENT ON TABLE table_name IS 'comment_text';
  ```
* **Example**:
  ```sql
  COMMENT ON TABLE Employees IS 'Stores information about full-time company employees.';
  ```

#### 1.6 RENAME
* **Description**: Renames an existing database object such as a table.
* **Syntax**:
  ```sql
  RENAME TABLE old_table_name TO new_table_name;
  ```
* **Example**:
  ```sql
  RENAME TABLE Employees TO StaffMembers;
  ```

---

### 2. Data Manipulation Language (DML)

DML commands are used to manage and manipulate actual data stored within database tables.

#### 2.1 INSERT
* **Description**: Inserts new data rows into a table.
* **Syntax**:
  ```sql
  INSERT INTO table_name (column1, column2, column3)
  VALUES (value1, value2, value3);
  ```
* **Example**:
  ```sql
  INSERT INTO Employees (EmpID, FirstName, Salary, HireDate)
  VALUES (101, 'Alex', 75000.00, '2024-01-15');
  ```

#### 2.2 UPDATE
* **Description**: Modifies existing data values in one or more table rows matching a condition.
* **Syntax**:
  ```sql
  UPDATE table_name
  SET column1 = value1, column2 = value2
  WHERE condition;
  ```
* **Example**:
  ```sql
  UPDATE Employees
  SET Salary = 82000.00
  WHERE EmpID = 101;
  ```

#### 2.3 DELETE
* **Description**: Removes existing rows from a table based on a condition.
* **Syntax**:
  ```sql
  DELETE FROM table_name WHERE condition;
  ```
* **Example**:
  ```sql
  DELETE FROM Employees WHERE EmpID = 101;
  ```

---

### 3. Transaction Control Language (TCL)

TCL commands manage database transactions to maintain ACID compliance and data integrity.

#### 3.1 BEGIN TRANSACTION
* **Description**: Marks the starting point of an explicit database transaction block.
* **Syntax**:
  ```sql
  BEGIN TRANSACTION;
  ```
* **Example**:
  ```sql
  BEGIN TRANSACTION;
  UPDATE Accounts SET Balance = Balance - 500 WHERE AccountID = 1;
  UPDATE Accounts SET Balance = Balance + 500 WHERE AccountID = 2;
  ```

#### 3.2 COMMIT
* **Description**: Saves all changes made during the current transaction permanently to the database.
* **Syntax**:
  ```sql
  COMMIT;
  ```
* **Example**:
  ```sql
  BEGIN TRANSACTION;
  UPDATE Accounts SET Balance = Balance - 500 WHERE AccountID = 1;
  UPDATE Accounts SET Balance = Balance + 500 WHERE AccountID = 2;
  COMMIT;
  ```

#### 3.3 ROLLBACK
* **Description**: Undoes all operations performed within the current transaction block, restoring data to its previous state.
* **Syntax**:
  ```sql
  ROLLBACK;
  ```
* **Example**:
  ```sql
  BEGIN TRANSACTION;
  DELETE FROM Orders WHERE OrderID = 50;
  -- Realized error, undo deletion:
  ROLLBACK;
  ```

#### 3.4 SAVEPOINT
* **Description**: Sets a checkpoint within a transaction so that you can selectively roll back to that specific point without reverting the entire transaction.
* **Syntax**:
  ```sql
  SAVEPOINT savepoint_name;
  ROLLBACK TO savepoint_name;
  ```
* **Example**:
  ```sql
  BEGIN TRANSACTION;
  INSERT INTO Logs VALUES ('Step 1 complete');
  SAVEPOINT Step1Done;

  INSERT INTO Logs VALUES ('Step 2 failed');
  -- Rollback only step 2:
  ROLLBACK TO Step1Done;
  COMMIT;
  ```

---

### 4. Data Query Language (DQL)

DQL commands are used to query, search, aggregate, and retrieve data from database tables.

#### 4.1 SELECT
* **Description**: Used to fetch data columns from one or more database tables.
* **Syntax**:
  ```sql
  SELECT column1, column2 FROM table_name;
  ```
* **Example**:
  ```sql
  SELECT FirstName, Salary FROM Employees;
  ```

#### 4.2 FROM
* **Description**: Specifies the target table(s) from which the query will read data.
* **Syntax**:
  ```sql
  SELECT * FROM table_name;
  ```
* **Example**:
  ```sql
  SELECT * FROM Employees;
  ```

#### 4.3 WHERE
* **Description**: Filters input rows before applying grouping or aggregation operations based on conditions.
* **Syntax**:
  ```sql
  SELECT * FROM table_name WHERE condition;
  ```
* **Example**:
  ```sql
  SELECT * FROM Employees WHERE Salary > 60000;
  ```

#### 4.4 GROUP BY
* **Description**: Groups rows sharing common column values together into summary rows.
* **Syntax**:
  ```sql
  SELECT column_name, COUNT(*)
  FROM table_name
  GROUP BY column_name;
  ```
* **Example**:
  ```sql
  SELECT Department, COUNT(*) AS TotalEmployees
  FROM Employees
  GROUP BY Department;
  ```

#### 4.5 HAVING
* **Description**: Filters aggregated results returned by a `GROUP BY` clause (functions like `WHERE` for aggregate functions).
* **Syntax**:
  ```sql
  SELECT column_name, AVG(salary)
  FROM table_name
  GROUP BY column_name
  HAVING AVG(salary) > threshold;
  ```
* **Example**:
  ```sql
  SELECT Department, AVG(Salary) AS AvgSalary
  FROM Employees
  GROUP BY Department
  HAVING AVG(Salary) > 70000;
  ```

#### 4.6 DISTINCT
* **Description**: Filters out duplicate values, returning only unique values in the query output.
* **Syntax**:
  ```sql
  SELECT DISTINCT column_name FROM table_name;
  ```
* **Example**:
  ```sql
  SELECT DISTINCT Department FROM Employees;
  ```

#### 4.7 ORDER BY
* **Description**: Sorts query result sets in ascending (`ASC`) or descending (`DESC`) order based on specified column(s).
* **Syntax**:
  ```sql
  SELECT * FROM table_name ORDER BY column_name [ASC|DESC];
  ```
* **Example**:
  ```sql
  SELECT FirstName, Salary FROM Employees ORDER BY Salary DESC;
  ```

#### 4.8 LIMIT
* **Description**: Restricts the maximum number of records returned in the result set (supported in PostgreSQL, MySQL, SQLite).
* **Syntax**:
  ```sql
  SELECT * FROM table_name LIMIT number;
  ```
* **Example**:
  ```sql
  SELECT * FROM Employees ORDER BY Salary DESC LIMIT 5;
  ```

---

### 5. Data Control Language (DCL)

DCL commands manage user privileges, permissions, and security controls within the database.

#### 5.1 GRANT
* **Description**: Provides specific access permissions and rights on database objects to specified users or roles.
* **Syntax**:
  ```sql
  GRANT privilege_name ON object_name TO user_name;
  ```
* **Example**:
  ```sql
  GRANT SELECT, INSERT ON Employees TO john_doe;
  ```

#### 5.2 REVOKE
* **Description**: Removes previously granted access privileges or permissions from specified users or roles.
* **Syntax**:
  ```sql
  REVOKE privilege_name ON object_name FROM user_name;
  ```
* **Example**:
  ```sql
  REVOKE INSERT ON Employees FROM john_doe;
  ```
