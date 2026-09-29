# SQL / RDBMS Using Oracle – Complete Notes
## BCA Semester 3

---

# UNIT 1 – Database Fundamentals & Data Types

## 1. Introduction
In modern software applications, storing, managing, and retrieving data efficiently is vital. A **Database System** provides a structured mechanism to handle data. 
- **SQL (Structured Query Language)** is the standard language used to interact with Relational Database Management Systems (RDBMS) like Oracle Database, MySQL, PostgreSQL, and MS SQL Server.
- Oracle Database is an enterprise-grade RDBMS that uses SQL alongside **SQL*Plus** (a command-line formatting tool) and **PL/SQL** (Procedural Language extension to SQL).

*Gujarati Explanation (70% English + 30% Gujarati):*
કોઈપણ સોફ્ટવેર કે કમ્પ્યુટર સિસ્ટમમાં ડેટાને સુરક્ષિત રીતે સ્ટોર કરવા અને ઝડપથી એક્સેસ કરવા માટે ડેટાબેઝનો ઉપયોગ થાય છે. SQL એ એક એવી Standard Language છે જેના દ્વારા આપણે Database સાથે વાતચીત (Query) કરી શકીએ છીએ. Oracle Database એ દુનિયાનું સૌથી પાવરફુલ RDBMS સોફ્ટવેર છે.

## 2. Important Definitions

1. **Data:** Unprocessed, raw facts, numbers, text, or symbols without context.
   - *Example:* `18`, `Darshan`, `Rajkot`
2. **Information:** Data that has been processed, structured, or contextualized to be meaningful and useful.
   - *Example:* *"Darshan is 18 years old and lives in Rajkot."*
3. **Database:** An organized collection of related data stored systematically in an electronic system so that it can be easily accessed, managed, updated, and queried.
4. **DBMS (Database Management System):** Software that interacts with end users, applications, and the database itself to capture, store, analyze, and retrieve data (e.g., MS Access, FileMaker).
5. **RDBMS (Relational Database Management System):** An advanced database system based on Edgar F. Codd's relational model, storing data in interconnected **Tables** (consisting of Rows and Columns) with predefined relationships between them (e.g., Oracle Database, MySQL).
6. **Table (Relation):** A structured grid composed of horizontal rows and vertical columns that holds related data within a database.
7. **Row / Record / Tuple:** A single horizontal entry in a table representing a single, complete record of an entity.
8. **Column / Field / Attribute:** A vertical entity in a table representing a specific attribute or property of the stored entity across all records.
9. **Primary Key:** A specific column (or combination of columns) that uniquely identifies each row/record in a table. It cannot contain duplicates or `NULL` values.
10. **Query:** A formal request or instruction sent to a database to retrieve, create, update, or remove data.
11. **Constraint:** Rules enforced on table columns to restrict the types of data that can be inserted, ensuring data accuracy and integrity.
12. **Data Type:** Defines the attribute of data stored in a column (e.g., Number, String, Date) specifying how the database engine handles and validates it.

*Gujarati Explanation:*
- **Data (ડેટા):** કાચા અને બિન-પ્રક્રિયા કરેલા આંકડા કે શબ્દો.
- **Information (માહિતી):** ડેટા પર પ્રોસેસ કરીને તૈયાર કરેલી ઉપયોગી વિગત.
- **Table (ટેબલ):** Rows (આડી હરોળ) અને Columns (ઊભી હરોળ) નું બનેલું સ્ટ્રક્ચર.
- **Row / Record (રેકોર્ડ):** ટેબલમાં રહેલી કોઈ એક આઈટમ કે વ્યક્તિની સંપૂર્ણ માહિતી (જેને Tuple પણ કહેવાય છે).
- **Primary Key:** ટેબલની એવી કોલમ જે દરેક રેકોર્ડને અલગ (Unique) પાડે છે અને તેમાં ક્યારેય કિંમત ખાલી (NULL) રહી શકતી નથી.

## 3. Concepts

### RDBMS Table Architecture
Consider the `students` table structure:

| id (Primary Key) | name | age | city |
| :--- | :--- | :--- | :--- |
| **101** | Darshan | 18 | Rajkot |
| **102** | Rahul | 20 | Ahmedabad |
| **103** | Priya | 19 | Surat |

- **Row (Tuple):** `101 | Darshan | 18 | Rajkot`
- **Column (Attribute):** `city` (values: Rajkot, Ahmedabad, Surat)

### SQL vs MySQL vs Oracle vs DBMS
| Term | Category | Role | Example |
| :--- | :--- | :--- | :--- |
| **SQL** | Language | Language used to interact with RDBMS | `SELECT * FROM table;` |
| **DBMS** | Concept | Software to manage databases | Access |
| **Oracle** | Software (RDBMS) | Enterprise relational database system | Oracle 19c / 21c |
| **MySQL** | Software (RDBMS) | Open-source relational database system | MySQL 8.0 |

### CRUD Operations Concept
In any RDBMS, all fundamental data operations fall into **4 categories (CRUD)**:
- **C – Create:** Adding new records (`INSERT`)
- **R – Read:** Fetching/Querying data (`SELECT`)
- **U – Update:** Modifying existing data (`UPDATE`)
- **D – Delete:** Removing unwanted records (`DELETE`)

### Oracle Data Types
Oracle supports standard data types categorized into Numeric, String, Date/Time, and LOBs:

1. **Numeric Data Types:**
   - `NUMBER(p, s)`: Stores fixed and floating-point numbers. `p` is precision (total digits), `s` is scale (digits right of decimal). e.g., `NUMBER(10, 2)` for currency like `15000.50`.
   - `INTEGER` / `INT`: Alias for `NUMBER(38, 0)`.

2. **String / Character Data Types:**
   - `CHAR(size)`: **Fixed-length** character string up to 2000 bytes. Blank pads remaining spaces.
   - `VARCHAR2(size)`: **Variable-length** character string up to 4000 bytes (Oracle specific). Does not waste space.
   - `NVARCHAR2(size)`: Variable-length Unicode string.

3. **Date / Time Data Types:**
   - `DATE`: Stores date and time (Year, Month, Day, Hour, Minute, Second). Default Oracle format is `DD-MON-YY` (e.g., `18-NOV-90`).
   - `TIMESTAMP`: Extension of `DATE` storing fractional seconds.

4. **LOB (Large Object) Data Types:**
   - `CLOB`: Character Large Object for storing massive text up to 4GB.
   - `BLOB`: Binary Large Object for storing images, audio, video up to 4GB.

### Type Conversions (Explicit Conversion Functions in Oracle)
- `TO_DATE('string', 'format')`: Converts character string to Date. e.g., `TO_DATE('18-11-1990', 'DD-MM-YYYY')`
- `TO_CHAR(date_or_number, 'format')`: Converts date or number to character string. e.g., `TO_CHAR(Hire_date, 'YYYY')`
- `TO_NUMBER('string')`: Converts string to numeric value.

*Gujarati Explanation (CHAR vs VARCHAR2):*
`CHAR(10)` માં જો તમે 'Raj' (3 અક્ષર) લખો, તો બાકીની 7 જગ્યાઓ ખાલી બાઇટ્સથી ભરાઈ જશે અને મેમરી વેસ્ટ થશે. પરંતુ `VARCHAR2(10)` માં 'Raj' લખતા તે માત્ર 3 અક્ષરની જ જગ્યા રોકશે. તેથી Oracle માં ડેટાબેઝ ડિઝાઇન કરતી વખતે `VARCHAR2` વાપરવું હિતાવહ છે.

## 4. SQL Commands
In Unit 1, the core data manipulation commands introduced are:
- `SELECT`: Reads and retrieves data rows from tables.
- `INSERT`: Adds new rows into a table.
- `UPDATE`: Modifies data values in existing rows.
- `DELETE`: Removes rows from a table.

## 5. Syntax

```sql
-- Single-line comment in Oracle SQL

/*
   Multi-line comment
   spans multiple lines
*/

-- Read Data
SELECT column1, column2 FROM table_name;

-- Insert Data
INSERT INTO table_name (col1, col2) VALUES (val1, val2);

-- Update Data
UPDATE table_name SET col1 = val1 WHERE condition;

-- Delete Data
DELETE FROM table_name WHERE condition;
```

## 6. Examples

```sql
-- Create Department Table
CREATE TABLE Department (
    Dept_no NUMBER(3) PRIMARY KEY,
    Depart_Name VARCHAR2(30) NOT NULL,
    Location VARCHAR2(30) NOT NULL
);

-- Create Employee Table
CREATE TABLE Employee (
    Emp_id NUMBER(6) PRIMARY KEY,
    Emp_name VARCHAR2(50) NOT NULL,
    Post VARCHAR2(30) NOT NULL,
    Mgr_id NUMBER(6),
    Hire_date DATE NOT NULL,
    Salary NUMBER(10, 2) NOT NULL,
    Commission NUMBER(10, 2),
    Dept_id NUMBER(3),
    CONSTRAINT fk_dept FOREIGN KEY (Dept_id) REFERENCES Department(Dept_no)
);

-- Insert Data with TO_DATE
INSERT INTO Department VALUES (10, 'IT', 'Anand');
INSERT INTO Employee VALUES (12345, 'BansiPadia', 'Clerk', NULL, TO_DATE('18-11-1990', 'DD-MM-YYYY'), 15000, NULL, 10);
COMMIT;
```

## 7. Important Points
1. SQL Keywords are **case-insensitive** (`SELECT` = `select`), but writing keywords in `UPPERCASE` is standard best practice.
2. Semicolon `;` terminates an SQL statement in Oracle SQL*Plus.
3. Primary Key must satisfy 2 strict rules:
   - Must be **UNIQUE** (No duplicate values).
   - Must be **NOT NULL** (Cannot be empty).
4. Oracle uses `VARCHAR2` instead of standard `VARCHAR`.
5. When inserting dates in custom formats, always use `TO_DATE('date_str', 'format')` to prevent implicit conversion errors.

## 8. Exam Questions
1. **What is the fundamental difference between Data and Information?**
   - *Answer:* Data consists of raw, unorganized facts (e.g., 18, Rajkot), whereas Information is processed, contextualized data that conveys meaning (e.g., Darshan is 18 years old and lives in Rajkot).
2. **What are the two alternate terms used for a Row and Column in RDBMS?**
   - *Row:* Record / Tuple
   - *Column:* Field / Attribute
3. **What is a Primary Key and what are its two mandatory rules?**
   - *Answer:* A Primary Key is a column or set of columns that uniquely identifies each row in a table. Rules: (1) Values must be unique. (2) Cannot contain NULL.
4. **Compare CHAR and VARCHAR2 data types in Oracle.**
   - *Answer:* `CHAR` is fixed-length (pads empty space with blanks), max 2000 bytes. `VARCHAR2` is variable-length (uses only actual content size), max 4000 bytes.
5. **What does CRUD stand for and which SQL command performs each operation?**
   - *C:* Create (`INSERT INTO`)
   - *R:* Read (`SELECT`)
   - *U:* Update (`UPDATE`)
   - *D:* Delete (`DELETE`)

---

# UNIT 2 – Data Definition Language (DDL) & Data Manipulation Language (DML)

## 1. Introduction
SQL operations are categorized into logical command groups based on their purpose:
- **DDL (Data Definition Language):** Defines, modifies, and drops the structure of database objects (tables, views, indexes). DDL changes structural metadata and is **auto-committed** in Oracle.
- **DML (Data Manipulation Language):** Handles data insertion, modification, and deletion within table rows. DML operations require explicit transaction control (`COMMIT` / `ROLLBACK`).

*Gujarati Explanation:*
DDL ટેબલના માળખા (Structure) સાથે કામ કરે છે (જેમ કે ટેબલ બનાવવું કે બિનજરૂરી ટેબલ ડીલીટ કરવું). DDL કમાન્ડ રન થતા જ આપોઆપ પર્મેનન્ટ (Auto-commit) થઈ જાય છે. જ્યારે DML ટેબલની અંદર રહેલા ડેટા (Rows) સાથે કામ કરે છે (જેમ કે નવો રેકોર્ડ ઉમેરવો કે સુધારવો). DML માં ફેરફાર સેવ કરવા માટે `COMMIT` કરવું પડે છે.

## 2. Important Definitions
1. **DDL (Data Definition Language):** A subset of SQL commands used to create, alter, drop, rename, and truncate database structures.
2. **DML (Data Manipulation Language):** A subset of SQL commands used to insert, update, delete, and merge data records inside database tables.
3. **Auto-commit:** Automatic permanent saving of transactions by the database engine without requiring a manual `COMMIT` command (All DDL commands auto-commit).
4. **Metadata:** "Data about data" — details regarding database table structure, column types, and constraints stored in the data dictionary.
5. **Truncate:** A fast DDL operation that removes all rows from a table and deallocates storage space without logging individual row deletions.
6. **Upsert (Merge):** A combined DML operation that updates existing records if a matching key exists, or inserts a new record if it does not exist.

## 3. Concepts

### DDL vs DML Detailed Comparison

| Parameter | DDL (Data Definition Language) | DML (Data Manipulation Language) |
| :--- | :--- | :--- |
| **Purpose** | Defines/alters database structure/schema. | Manipulates table data records. |
| **Commands** | `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME` | `INSERT`, `UPDATE`, `DELETE`, `MERGE` |
| **Effect** | Affects table metadata / structure. | Affects rows/tuples inside table. |
| **Auto-Commit** | Yes (Executed changes are immediately permanent). | No (Requires explicit `COMMIT` or `ROLLBACK`). |
| **Rollback** | Cannot be rolled back. | Can be rolled back before `COMMIT`. |

### Difference Between DROP, TRUNCATE, and DELETE

| Command | Command Type | Purpose | Rollback Possible? | Space Recovery |
| :--- | :--- | :--- | :--- | :--- |
| **`DELETE`** | DML | Removes specific or all rows based on `WHERE` clause. | Yes (Before `COMMIT`) | No (Keeps high-water mark) |
| **`TRUNCATE`** | DDL | Fast removal of ALL rows from table. | No (Auto-commit) | Yes (Resets storage space) |
| **`DROP`** | DDL | Deletes table structure completely along with all data. | No (Auto-commit) | Yes (Frees total space) |

*Gujarati Explanation (DROP vs TRUNCATE vs DELETE):*
- `DELETE`: ચોપડીમાંથી અમુક પાના ફાડી નાખવા (Rollback શક્ય છે).
- `TRUNCATE`: ચોપડીના બધા પાના એકસાથે ખાલી કરી નાખવા પણ પૂંઠું રહેવા દેવું (Rollback શક્ય નથી).
- `DROP`: આખી ચોપડી જ સળગાવી દેવી/નાશ કરવો (ટેબલ જ જતું રહે).

## 4. SQL Commands
### DDL Commands:
- `CREATE`: Creates a new table, view, index, or sequence.
- `ALTER`: Modifies structure of an existing table (Add/Modify/Drop columns).
- `DROP`: Permanently deletes an object from the database.
- `TRUNCATE`: Removes all data rows from a table while maintaining structure.
- `RENAME`: Renames a database object.

### DML Commands:
- `INSERT`: Adds new data rows into a table.
- `UPDATE`: Modifies existing row values.
- `DELETE`: Deletes specific or all rows from a table.
- `MERGE`: Conditional insert/update (Upsert).

## 5. Syntax

```sql
-- DDL Syntax
CREATE TABLE table_name (column1 data_type, column2 data_type);
ALTER TABLE table_name ADD (new_column data_type);
ALTER TABLE table_name MODIFY (column_name new_data_type);
ALTER TABLE table_name DROP COLUMN column_name;
ALTER TABLE table_name RENAME COLUMN old_name TO new_name;
RENAME old_table_name TO new_table_name;
TRUNCATE TABLE table_name;
DROP TABLE table_name;

-- DML Syntax
INSERT INTO table_name VALUES (val1, val2);
UPDATE table_name SET col1 = val1 WHERE condition;
DELETE FROM table_name WHERE condition;
```

## 6. Examples

```sql
-- Student Table Creation
CREATE TABLE Student (
    Rollno NUMBER(5) PRIMARY KEY,
    name VARCHAR2(50) NOT NULL,
    city VARCHAR2(30) NOT NULL,
    address VARCHAR2(100),
    DOB DATE NOT NULL,
    age NUMBER(3) NOT NULL,
    class VARCHAR2(20) NOT NULL,
    mobileno VARCHAR2(15)
);

-- Insert Record
INSERT INTO Student VALUES (1, 'Amit Shah', 'Rajkot', '123 Ring Road', TO_DATE('15-05-2006', 'DD-MM-YYYY'), 18, 'Sem-3', '9876543210');

-- Update Query
UPDATE Student 
SET city = 'Jamnagar' 
WHERE LOWER(city) = 'rajkot';

-- Delete Query
DELETE FROM Student 
WHERE age > 20;

COMMIT;
```

## 7. Important Points
1. Always include a `WHERE` clause in `UPDATE` and `DELETE` queries, otherwise **ALL rows in the table will be modified or deleted!**
2. DDL commands auto-commit instantly in Oracle SQL. Executing `CREATE` or `ALTER` automatically commits any pending DML operations as well!
3. To delete all rows quickly and free allocated disk space, prefer `TRUNCATE TABLE` over `DELETE FROM`.
4. Column data type modifications (`ALTER TABLE MODIFY`) are only permitted if the column contains all NULLs or if changing to compatible size extensions.

## 8. Exam Questions
1. **Differentiate between DDL and DML commands with examples.**
   - *Answer:* DDL defines table schema (`CREATE`, `ALTER`, `DROP`) and auto-commits. DML manipulates row data (`INSERT`, `UPDATE`, `DELETE`) and requires explicit commit.
2. **Compare DROP, TRUNCATE, and DELETE commands in SQL.**
   - *Answer:* `DELETE` is DML (removes specific rows, rollback possible). `TRUNCATE` is DDL (removes all rows fast, resets space, no rollback). `DROP` is DDL (removes entire table schema and data).
3. **Write an Oracle SQL command to add a column `email VARCHAR2(50)` to an existing table `Student`.**
   - `ALTER TABLE Student ADD (email VARCHAR2(50));`
4. **What happens if you execute `UPDATE Student SET city = 'Surat';` without a WHERE clause?**
   - *Answer:* The `city` column for every single student record in the table will be overwritten with 'Surat'.

---

# UNIT 3 – Data Query Language (DQL), Operators, Conditions & SQL Functions

## 1. Introduction
Data retrieval is the most frequent database activity. **DQL (Data Query Language)** centers around the `SELECT` statement. This unit covers record filtering with `WHERE`, pattern matching, conditional operators, sorting with `ORDER BY`, single-row functions (String, Math, Date), aggregate functions, and grouping operations (`GROUP BY` and `HAVING`).

*Gujarati Explanation:*
જ્યારે ડેટાબેઝમાંથી ચોક્કસ ડેટા શોધવો હોય કે રિપોર્ટ બનાવવો હોય ત્યારે DQL ના `SELECT` કમાન્ડનો ઉપયોગ થાય છે. આ યુનિટમાં આપણે અલગ અલગ ઓપરેટર્સ (`BETWEEN`, `LIKE`, `IN`), ફંક્શન્સ (`COUNT`, `SUM`, `AVG`), તેમજ ડેટાનું ગ્રુપ બનાવીને રિપોર્ટ કાઢવાના કમાન્ડ્સ (`GROUP BY`, `HAVING`) શીખીશું.

## 2. Important Definitions
1. **DQL (Data Query Language):** SQL commands focused on querying and fetching data from database tables (`SELECT`).
2. **Projection:** Selecting specific columns from a table in a query.
3. **Selection / Filtering:** Retrieving specific rows that satisfy given logical criteria (`WHERE`).
4. **Null Value:** Representing absent, unknown, or unassigned data in a column. Null is NOT equal to zero `0` or empty space `' '`.
5. **Aggregate Function:** A function that takes multiple column values across rows and returns a single summary result (e.g., `SUM`, `AVG`, `COUNT`).
6. **Single-Row Function:** A function that operates on an individual row value and returns one result per row (e.g., `UPPER`, `LENGTH`, `ROUND`).
7. **Pattern Matching:** Filtering text values using wildcard characters (`%` and `_`) with the `LIKE` operator.

## 3. Concepts

### Execution Order of an SQL Query
When an SQL query executes, Oracle processes clauses in the following mandatory order:
1. `FROM` (Identify target table)
2. `WHERE` (Filter raw individual rows)
3. `GROUP BY` (Group filtered rows)
4. `HAVING` (Filter aggregated groups)
5. `SELECT` (Project output columns)
6. `ORDER BY` (Sort final output rows)

### WHERE Clause vs HAVING Clause Comparison

| Parameter | WHERE Clause | HAVING Clause |
| :--- | :--- | :--- |
| **Purpose** | Filters individual records/rows before grouping. | Filters groups after `GROUP BY` execution. |
| **Placement** | Placed before `GROUP BY`. | Placed after `GROUP BY`. |
| **Aggregate Functions**| **NOT allowed** (e.g., `WHERE SUM(sal) > 5000` is invalid). | **Allowed** (e.g., `HAVING SUM(sal) > 5000`). |

### Wildcard Characters with LIKE Operator
- `%` (Percent): Represents zero, one, or multiple characters.
  - *Example:* `'K%'` matches 'K', 'Karan', 'Kalpana'.
- `_` (Underscore): Represents exactly one single character.
  - *Example:* `'A_i'` matches 'Ali', 'Ani'.

### Single-Row Functions vs Aggregate Functions
- **Single-Row Functions:**
  - *String Functions:* `LOWER(str)`, `UPPER(str)`, `INITCAP(str)`, `LENGTH(str)`, `SUBSTR(str, pos, len)`, `CONCAT(str1, str2)`.
  - *Numeric Functions:* `ROUND(val, dec)`, `TRUNC(val, dec)`, `MOD(n, m)`, `ABS(val)`.
  - *Date Functions:* `SYSDATE` (Current system date), `ADD_MONTHS(date, n)`, `MONTHS_BETWEEN(d1, d2)`, `EXTRACT(unit FROM date)`.
  - *General Functions:* `NVL(expr1, expr2)` replaces NULL in `expr1` with `expr2`.
- **Aggregate Functions:**
  - `COUNT(*)` / `COUNT(col)`: Counts rows/non-null values.
  - `SUM(col)`: Calculates total sum of numeric values.
  - `AVG(col)`: Calculates average of numeric values.
  - `MIN(col)` / `MAX(col)`: Finds minimum / maximum value.

## 4. SQL Commands
- `SELECT`: Column projection and data fetching.
- `WHERE`: Row filtering.
- `DISTINCT`: Eliminates duplicate values in output.
- `ORDER BY`: Sorts results (`ASC` for ascending, `DESC` for descending).
- `GROUP BY`: Groups rows possessing identical values in specified columns.
- `HAVING`: Filters aggregated group results.

### SQL Operators:
- **Relational / Comparison:** `=`, `!=`, `<>`, `<`, `>`, `<=`, `>=`
- **Logical:** `AND`, `OR`, `NOT`
- **Special Filtering:** `BETWEEN val1 AND val2`, `IN (list)`, `LIKE 'pattern'`, `IS NULL`, `IS NOT NULL`

## 5. Syntax

```sql
SELECT DISTINCT column1, column2, AGGREGATE_FUNCTION(column3)
FROM table_name
WHERE condition
GROUP BY column1, column2
HAVING aggregate_condition
ORDER BY column1 ASC|DESC;
```

## 6. Examples

```sql
-- Filter by LIKE
SELECT * FROM Employee WHERE LOWER(Post) = 'salesman' AND Emp_name LIKE 'K%';

-- Filter by BETWEEN
SELECT * FROM Employee WHERE Salary BETWEEN 20000 AND 90000;

-- Aggregate function with GROUP BY & HAVING
SELECT Dept_id, COUNT(*) AS Total_Emp, AVG(Salary) AS Avg_Sal
FROM Employee
GROUP BY Dept_id
HAVING AVG(Salary) > 20000;
```

## 7. Important Points
1. In Oracle SQL, string comparisons are case-sensitive. Using `LOWER(col)` or `UPPER(col)` prevents case mismatch issues.
2. `WHERE` clause cannot contain aggregate functions like `WHERE SUM(sal) > 5000` (Use `HAVING` instead).
3. `COUNT(*)` counts all rows including NULLs, whereas `COUNT(column_name)` ignores `NULL` values.
4. `NVL(Commission, 0)` is essential when performing mathematical operations on nullable columns because `NUMBER + NULL = NULL`.

## 8. Exam Questions
1. **Explain the difference between WHERE and HAVING clause.**
   - *Answer:* `WHERE` filters individual records before grouping and cannot contain aggregate functions. `HAVING` filters group results after `GROUP BY` and allows aggregate functions.
2. **Explain wildcards used with the LIKE operator.**
   - *Answer:* `%` matches zero or more characters. `_` matches exactly one single character.
3. **What is the purpose of NVL() function in Oracle? Give an example.**
   - *Answer:* `NVL(expr1, expr2)` replaces NULL values in `expr1` with `expr2`. Example: `SELECT Salary + NVL(Commission, 0) FROM Employee;`.
4. **What is the difference between COUNT(*) and COUNT(column_name)?**
   - *Answer:* `COUNT(*)` counts total rows in the result set including NULL rows, while `COUNT(column_name)` counts only non-null values in that column.

---

# UNIT 4 – Constraints, Joins & Subqueries

## 1. Introduction
To ensure data integrity and prevent invalid data entry, RDBMS uses **Constraints**. To fetch data spread across multiple linked tables, **SQL Joins** combine tables based on matching columns. When complex queries require nested data evaluations, **Subqueries (Inner Queries)** allow embedding one `SELECT` statement inside another.

*Gujarati Explanation:*
- **Constraints (નિયમો):** ટેબલમાં ખોટો ડેટા દાખલ થતો અટકાવવા માટેના નિયમો (જેમ કે ઉંમર 18 થી વધારે જ હોવી જોઈએ).
- **Joins (જોઇન્સ):** જ્યારે બે કે તેથી વધુ ટેબલમાંથી ભેગો ડેટા લાવવો હોય ત્યારે Foreign Key ની મદદથી ટેબલ જોડવાની પદ્ધતિ.
- **Subqueries (સબક્વેરી):** એક ક્વેરીની અંદર બીજી ક્વેરી લખવી.

## 2. Important Definitions
1. **Constraint:** Rules enforced on data columns of a table to maintain data accuracy, reliability, and integrity.
2. **Primary Key Constraint:** Enforces uniqueness and NOT NULL on a column to uniquely identify each row.
3. **Foreign Key Constraint:** A field in one table that references the Primary Key of another table, establishing a referential integrity link.
4. **Referential Integrity:** A database property ensuring that foreign key relationships between tables remain consistent (no orphan child records).
5. **Join:** An operation combining columns from one or more tables using values common to each.
6. **Inner Join:** Returns only the matching rows between both tables.
7. **Outer Join (Left / Right / Full):** Returns matching rows plus unmatched rows from the left, right, or both tables filled with NULLs.
8. **Subquery (Nested / Inner Query):** A `SELECT` statement embedded inside a `WHERE`, `HAVING`, or `FROM` clause of an outer query.
9. **Correlated Subquery:** A subquery that depends on values supplied by the outer query for each processed row.

## 3. Concepts

### Constraint Types in Oracle
1. `NOT NULL`: Prevents column from accepting NULL values.
2. `UNIQUE`: Ensures all values in a column are distinct.
3. `PRIMARY KEY`: Uniquely identifies each record (`UNIQUE` + `NOT NULL`).
4. `FOREIGN KEY`: Maintains referential integrity by referencing Primary Key in parent table.
5. `CHECK`: Validates that column values satisfy a specific boolean condition.
6. `DEFAULT`: Assigns a default value if no value is explicitly supplied.

### Types of SQL Joins
1. **`INNER JOIN`:** Returns rows having matching values in both tables.
2. **`LEFT JOIN` (Left Outer Join):** Returns all rows from left table and matching rows from right table.
3. **`RIGHT JOIN` (Right Outer Join):** Returns all rows from right table and matching rows from left table.
4. **`FULL JOIN` (Full Outer Join):** Returns all rows when there is a match in either left or right table.
5. **`CROSS JOIN`:** Returns Cartesian product of two tables (rows in A × rows in B).
6. **`SELF JOIN`:** A table joined with itself using table aliases.

### Subquery Concepts
- **Single-Row Subquery:** Returns 1 row; uses single-row operators (`=`, `>`, `<`, `>=`, `<=`, `!=`).
- **Multi-Row Subquery:** Returns multiple rows; uses multi-row operators (`IN`, `ANY`, `ALL`).
- **EXISTS Operator:** Returns `TRUE` if subquery returns one or more rows.

## 4. SQL Commands
- `CONSTRAINT constraint_name`: Declares explicit named constraint.
- `REFERENCES parent_table(primary_key_col)`: Establishes Foreign Key linkage.
- `ON DELETE CASCADE`: Automatically deletes child rows when parent row is deleted.
- `INNER JOIN / LEFT JOIN / RIGHT JOIN / FULL JOIN ... ON`: Table joining syntax.
- `IN`, `ANY`, `ALL`, `EXISTS`, `NOT EXISTS`: Subquery logical operators.
- `UNION`, `INTERSECT`, `MINUS`: Set operators for combining query outputs.

## 5. Syntax

```sql
-- Foreign Key Creation
CREATE TABLE Child_Table (
    child_id NUMBER PRIMARY KEY,
    parent_id NUMBER,
    CONSTRAINT fk_child_parent FOREIGN KEY (parent_id) 
        REFERENCES Parent_Table(parent_id) ON DELETE CASCADE
);

-- Inner Join Syntax
SELECT a.col1, b.col2 
FROM TableA a 
JOIN TableB b ON a.common_id = b.common_id;

-- Subquery Syntax
SELECT * FROM TableA 
WHERE col1 IN (SELECT col1 FROM TableB WHERE condition);
```

## 6. Examples

```sql
-- Join Example (Student_Master & Course_master)
SELECT c.c_name AS Course_Name, s.Sno, s.sname AS Student_Name, s.city, s.age 
FROM Student_Master s 
JOIN Course_master c ON s.c_code = c.C_code 
ORDER BY c.c_name, s.sname;

-- Subquery Example
SELECT * FROM Emp 
WHERE salary > (SELECT salary FROM Emp WHERE LOWER(ename) = 'amar')
  AND salary < (SELECT salary FROM Emp WHERE LOWER(ename) = 'karan');

-- Set Operator INTERSECT Example
SELECT cname FROM Customer WHERE LOWER(city) = 'nagpur'
INTERSECT
SELECT cname FROM Deposit
INTERSECT
SELECT cname FROM Borrow;
```

## 7. Important Points
1. A Foreign Key column can contain `NULL` values unless `NOT NULL` is explicitly added.
2. A table can have **only ONE Primary Key**, but multiple `UNIQUE` constraints.
3. Subqueries inside `WHERE` clauses must be enclosed in parentheses `()`.
4. Using `ON DELETE CASCADE` on foreign keys automatically cleans up child records when a parent record is removed.

## 8. Exam Questions
1. **What is Referential Integrity? How is it maintained in SQL?**
   - *Answer:* Referential Integrity ensures relationships between tables remain valid. It is enforced using Foreign Key constraints referencing a parent table's Primary Key.
2. **Differentiate between INNER JOIN and LEFT JOIN.**
   - *Answer:* `INNER JOIN` returns only rows matching in both tables. `LEFT JOIN` returns all rows from the left table regardless of matching rows in the right table.
3. **Explain Single-row vs Multi-row subqueries.**
   - *Answer:* Single-row subqueries return 1 value and use comparison operators (`=`, `>`). Multi-row subqueries return multiple values and require operators like `IN`, `ANY`, `ALL`.
4. **What is the purpose of ON DELETE CASCADE clause?**
   - *Answer:* It automatically deletes child table rows when the corresponding parent table row is deleted.

---

# UNIT 5 – Database Objects, DCL, TCL, Oracle SQL*Plus & PL/SQL

## 1. Introduction
Beyond standard tables, Oracle RDBMS provides database objects such as **Views** (virtual tables), **Indexes** (search performance boosters), **Sequences** (auto-increment counter generators), and **Synonyms** (alias names). Database control is governed by **DCL (GRANT/REVOKE)** for access security and **TCL (COMMIT/ROLLBACK/SAVEPOINT)** for transactional reliability (ACID properties). SQL*Plus is Oracle's formatting and reporting environment, while **PL/SQL** adds procedural control (loops, variables, conditions, triggers, procedures) to SQL.

*Gujarati Explanation:*
આ યુનિટમાં આપણે ઑબ્જેક્ટ્સ (Views, Indexes, Sequences), સુરક્ષા માટે DCL કમાન્ડ્સ, ટ્રાન્ઝેક્શન કંટ્રોલ (TCL - COMMIT, ROLLBACK), SQL*Plus માં રિપોર્ટ ડિઝાઇન કરવા અને PL/SQL પ્રોગ્રામિંગ ના મૂળભૂત ખ્યાલો શીખીશું.

## 2. Important Definitions
1. **View:** A virtual table based on the result-set of an SQL statement. It does not store physical data itself.
2. **Index:** A database object created on table columns to speed up data retrieval queries (using B-Tree structures).
3. **Sequence:** A database object used to generate unique, sequential numeric values (ideal for primary keys).
4. **Synonym:** An alternative permanent alias name assigned to a table, view, sequence, or procedure.
5. **DCL (Data Control Language):** SQL commands (`GRANT`, `REVOKE`) managing privileges and database access rights.
6. **TCL (Transaction Control Language):** SQL commands managing database transactions (`COMMIT`, `ROLLBACK`, `SAVEPOINT`).
7. **Transaction:** A single logical unit of work consisting of one or more SQL statements executed indivisibly.
8. **ACID Properties:** Four essential transaction guarantees: Atomicity, Consistency, Isolation, and Durability.
9. **PL/SQL (Procedural Language/SQL):** Oracle's block-structured procedural extension to SQL featuring variables, loops, conditionals, cursors, and triggers.
10. **Pseudo-columns:** Special Oracle system columns (`ROWNUM`, `ROWID`, `DUAL`) that behave like table columns but are managed by Oracle engine.

## 3. Concepts

### Database Objects Overview
- **View:** Virtual table based on `SELECT`. Used for security and simplifying complex queries.
- **Index:** B-Tree structure on disk. Used to speed up `SELECT` queries.
- **Sequence:** Numeric counter. Used for auto-incrementing Primary Keys.
- **Synonym:** Alias name for database objects.

### Transaction ACID Properties
- **Atomicity:** All or nothing execution.
- **Consistency:** Database transitions validly from one consistent state to another.
- **Isolation:** Concurrent transactions execute independently.
- **Durability:** Committed changes persist permanently.

### PL/SQL Block Structure

```sql
DECLARE
    -- Declaration section (Variables, Constants, Cursors)
BEGIN
    -- Executable section (SQL & PL/SQL statements)
EXCEPTION
    -- Exception handling section (Error management)
END;
/
```

## 4. SQL Commands & Keywords
- `CREATE VIEW view_name AS SELECT ...`
- `CREATE INDEX index_name ON table(column)`
- `CREATE SEQUENCE sequence_name START WITH 1 INCREMENT BY 1`
- `CREATE SYNONYM synonym_name FOR object_name`
- `GRANT privilege ON object TO user`
- `REVOKE privilege ON object FROM user`
- `COMMIT`: Saves changes permanently.
- `ROLLBACK`: Undoes uncommitted changes.
- `SAVEPOINT savepoint_name`: Creates a checkpoint within a transaction.

## 5. Syntax

```sql
-- View Syntax
CREATE VIEW emp_view AS SELECT Emp_name, Salary FROM Employee WHERE Dept_id = 10;

-- Index Syntax
CREATE INDEX idx_emp_name ON Employee(Emp_name);

-- Sequence Syntax
CREATE SEQUENCE emp_seq START WITH 100 INCREMENT BY 1 NOCACHE;

-- Grant & Revoke Syntax
GRANT SELECT, INSERT ON Employee TO user1;
REVOKE INSERT ON Employee FROM user1;

-- TCL Syntax
SAVEPOINT sp1;
ROLLBACK TO sp1;
COMMIT;
```

## 6. Examples

```sql
-- SQL*Plus Report Script Example
CLEAR COLUMNS
CLEAR BREAKS
CLEAR COMPUTES
SET PAGESIZE 30
SET LINESIZE 80
TTITLE CENTER 'ORDER DETAIL REPORT' SKIP 2
COLUMN Item_price HEADING 'Price (Rs)' FORMAT 99,99,990.00
BREAK ON REPORT
COMPUTE SUM LABEL 'TOTAL SUM:' OF Item_price ON REPORT

SELECT Order_no, TO_CHAR(Order_date, 'DD-Mon-YYYY') AS Order_date, Item, Item_price, Discount 
FROM Order_detail;

-- PL/SQL Anonymous Block Example
DECLARE
    v_emp_name Employee.Emp_name%TYPE;
    v_salary   Employee.Salary%TYPE;
BEGIN
    SELECT Emp_name, Salary INTO v_emp_name, v_salary FROM Employee WHERE Emp_id = 12345;
    DBMS_OUTPUT.PUT_LINE('Employee Name: ' || v_emp_name || ', Salary: ' || v_salary);
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee found!');
END;
/
```

## 7. Important Points
1. Views do NOT store data on disk; they dynamically re-run their underlying `SELECT` query whenever called.
2. Creating indexes speeds up read queries (`SELECT`), but slightly slows down `INSERT`, `UPDATE`, and `DELETE` operations.
3. Sequence values are retrieved using `sequence_name.NEXTVAL` and `sequence_name.CURRVAL`.
4. `ROLLBACK` without specifying a savepoint reverts the database all the way back to the last executed `COMMIT`.

## 8. Exam Questions
1. **What is a View? State its advantages.**
   - *Answer:* A View is a virtual table defined by a `SELECT` query. Advantages: (1) Enhances data security. (2) Simplifies complex queries.
2. **What is an Index? When should you create an Index?**
   - *Answer:* An Index is a database object that accelerates search performance. Create indexes on columns frequently used in `WHERE`, `JOIN`, and `ORDER BY` clauses.
3. **Explain ACID properties of a Database Transaction.**
   - *Answer:* Atomicity (All or nothing), Consistency (State validity), Isolation (Independent execution), Durability (Permanent committed changes).
4. **Write PL/SQL block structure and explain its sections.**
   - *Answer:* `DECLARE` (variables), `BEGIN` (executables), `EXCEPTION` (error handling), `END;` (termination).

---

# SQL COMMANDS – QUICK REFERENCE

### 1. CREATE TABLE
- **Purpose:** Creates a new table in the database with defined columns, data types, and integrity constraints.
- **Syntax:**
  ```sql
  CREATE TABLE table_name (
      column1 data_type [CONSTRAINT constraint_name],
      column2 data_type
  );
  ```
- **Example:**
  ```sql
  CREATE TABLE Department (
      Dept_no NUMBER(3) PRIMARY KEY,
      Depart_Name VARCHAR2(30) NOT NULL
  );
  ```
- **Important Note:** A DDL command that auto-commits instantly. Table name must be unique within schema.

### 2. ALTER TABLE
- **Purpose:** Modifies structural definition of an existing table.
- **Syntax:**
  ```sql
  ALTER TABLE table_name ADD (new_column data_type);
  ALTER TABLE table_name MODIFY (column_name new_data_type);
  ALTER TABLE table_name DROP COLUMN column_name;
  ```
- **Example:**
  ```sql
  ALTER TABLE Employee ADD (email VARCHAR2(50));
  ```
- **Important Note:** DDL operation that auto-commits changes.

### 3. DROP TABLE
- **Purpose:** Permanently deletes an entire table schema along with all stored data.
- **Syntax:**
  ```sql
  DROP TABLE table_name [CASCADE CONSTRAINTS];
  ```
- **Example:**
  ```sql
  DROP TABLE Student;
  ```
- **Important Note:** DDL operation that CANNOT be rolled back!

### 4. TRUNCATE TABLE
- **Purpose:** Fast removal of ALL data rows from a table while preserving structure.
- **Syntax:**
  ```sql
  TRUNCATE TABLE table_name;
  ```
- **Example:**
  ```sql
  TRUNCATE TABLE Order_detail;
  ```
- **Important Note:** Faster than `DELETE` because it deallocates storage space and resets high-water mark without undo logs.

### 5. RENAME
- **Purpose:** Changes the name of an existing table or object.
- **Syntax:**
  ```sql
  RENAME old_name TO new_name;
  ```
- **Example:**
  ```sql
  RENAME Emp TO Employee_Master;
  ```
- **Important Note:** DDL operation that auto-commits.

### 6. INSERT INTO
- **Purpose:** Adds new data rows into a database table.
- **Syntax:**
  ```sql
  INSERT INTO table_name (col1, col2) VALUES (val1, val2);
  ```
- **Example:**
  ```sql
  INSERT INTO Department VALUES (10, 'IT', 'Anand');
  ```
- **Important Note:** DML operation. Changes are transient until explicitly saved using `COMMIT`.

### 7. UPDATE
- **Purpose:** Modifies values of existing records in a table based on filtering conditions.
- **Syntax:**
  ```sql
  UPDATE table_name SET column1 = value1 WHERE condition;
  ```
- **Example:**
  ```sql
  UPDATE Student SET city = 'Jamnagar' WHERE LOWER(city) = 'rajkot';
  ```
- **Important Note:** Always use a `WHERE` clause; omitting `WHERE` updates every single row in the table!

### 8. DELETE FROM
- **Purpose:** Removes specific or all data rows from a table based on a condition.
- **Syntax:**
  ```sql
  DELETE FROM table_name WHERE condition;
  ```
- **Example:**
  ```sql
  DELETE FROM Student WHERE age > 20;
  ```
- **Important Note:** DML operation. Can be reversed using `ROLLBACK` before commit.

### 9. SELECT
- **Purpose:** Queries and fetches data records from one or more tables.
- **Syntax:**
  ```sql
  SELECT [DISTINCT] col1, col2 FROM table_name WHERE condition ORDER BY col1 ASC|DESC;
  ```
- **Example:**
  ```sql
  SELECT Emp_name, Salary FROM Employee WHERE Dept_id = 10;
  ```
- **Important Note:** The primary DQL query command. Does not mutate stored data.

### 10. GRANT
- **Purpose:** Bestows administrative permissions or specific table privileges to users.
- **Syntax:**
  ```sql
  GRANT privilege_list ON object_name TO user_name;
  ```
- **Example:**
  ```sql
  GRANT SELECT, INSERT ON Employee TO user1;
  ```
- **Important Note:** DCL security command.

### 11. REVOKE
- **Purpose:** Withdraws previously granted privileges from a user or role.
- **Syntax:**
  ```sql
  REVOKE privilege_list ON object_name FROM user_name;
  ```
- **Example:**
  ```sql
  REVOKE INSERT ON Employee FROM user1;
  ```
- **Important Note:** DCL command that immediately removes rights.

### 12. COMMIT
- **Purpose:** Permanently saves all pending DML transaction modifications to disk storage.
- **Syntax:**
  ```sql
  COMMIT;
  ```
- **Example:**
  ```sql
  COMMIT;
  ```
- **Important Note:** Ends current transaction. Once committed, changes cannot be undone via `ROLLBACK`.

### 13. ROLLBACK
- **Purpose:** Reverts uncommitted DML data changes back to the start of the transaction or to a designated savepoint.
- **Syntax:**
  ```sql
  ROLLBACK [TO savepoint_name];
  ```
- **Example:**
  ```sql
  ROLLBACK TO sp1;
  ```
- **Important Note:** Undoes temporary updates and releases row locks.

### 14. SAVEPOINT
- **Purpose:** Creates a named intermediate marker within a transaction to allow partial rollbacks.
- **Syntax:**
  ```sql
  SAVEPOINT savepoint_name;
  ```
- **Example:**
  ```sql
  SAVEPOINT sp1;
  ```
- **Important Note:** Enables granular transaction recovery control without aborting entire transaction.

### 15. MERGE (UPSERT)
- **Purpose:** Performs conditional insert and update operations in a single atomic SQL statement based on key matching.
- **Syntax:**
  ```sql
  MERGE INTO target_table t
  USING source_table s ON (t.id = s.id)
  WHEN MATCHED THEN UPDATE SET t.col = s.col
  WHEN NOT MATCHED THEN INSERT (id, col) VALUES (s.id, s.col);
  ```
- **Example:** Updates existing customer record or inserts new record if ID does not exist.
- **Important Note:** Highly efficient for bulk synchronization operations.

---

# SQL*PLUS COMMANDS

Oracle **SQL*Plus** is a command-line interface tool used to execute SQL statements, run PL/SQL blocks, and format custom database reports.

### Summary of SQL*Plus Environment & Formatting Commands

1. `DESC table_name;`
   - *Description:* Displays column schema definitions, data types, and nullability constraints of a table.
   - *Example:* `DESC Employee;`

2. `SET PAGESIZE n`
   - *Description:* Configures the number of lines displayed per page before printing header titles again.
   - *Example:* `SET PAGESIZE 30`

3. `SET LINESIZE n`
   - *Description:* Configures horizontal line character width before wrapping text.
   - *Example:* `SET LINESIZE 80`

4. `TTITLE`
   - *Description:* Sets Top Page Title text with alignment formatting (`CENTER`, `LEFT`, `RIGHT`, `SKIP`).
   - *Example:* `TTITLE CENTER 'ORDER DETAIL REPORT' SKIP 2`

5. `COLUMN`
   - *Description:* Formats individual column headings and display widths (`FORMAT A12` for string width, `FORMAT 99,99,990.00` for currency numbers).
   - *Example:* `COLUMN Item_price HEADING 'Price (Rs)' FORMAT 99,99,990.00`

6. `BREAK ON`
   - *Description:* Suppresses repeating values in a column or breaks report execution for summary aggregation.
   - *Example:* `BREAK ON REPORT`

7. `COMPUTE`
   - *Description:* Calculates mathematical aggregate summary values (e.g., `SUM`, `AVG`) at defined break points.
   - *Example:* `COMPUTE SUM LABEL 'TOTAL SUM:' OF Item_price ON REPORT`

8. `CLEAR COLUMNS / BREAKS / COMPUTES`
   - *Description:* Clears previous report formatting settings in the SQL*Plus session buffer.
   - *Example:* `CLEAR COLUMNS`

9. `DUAL Table Queries`
   - *Description:* `DUAL` is Oracle's built-in 1-row, 1-column pseudo-table used for evaluating expressions and functions.
   - *Example:* `SELECT SYSDATE FROM DUAL;`

10. `ROWNUM & ROWID Pseudo-columns`
    - *Description:* `ROWNUM` returns row position numbers in result sets; `ROWID` returns physical disk address of rows.
    - *Example:* `SELECT ROWNUM, Emp_name FROM Employee WHERE ROWNUM <= 5;`

---

# SQL 0% → 100% PRACTICAL ROADMAP

## Level 0–10%
- Database Fundamentals (Data, Information, Database, DBMS vs RDBMS)
- RDBMS Table Architecture (Rows/Tuples, Columns/Attributes, Primary Key)
- SQL Overview, SQL Syntax rules, Comments (`--`, `/* */`)
- Core CRUD Operations mapping (`INSERT`, `SELECT`, `UPDATE`, `DELETE`)

## Level 10–20%
- Oracle Data Types (`NUMBER`, `CHAR`, `VARCHAR2`, `DATE`, `TIMESTAMP`, `CLOB`, `BLOB`)
- Explicit Conversion Functions (`TO_DATE`, `TO_CHAR`, `TO_NUMBER`)
- Basic `CREATE TABLE` and `INSERT INTO` scripts with `TO_DATE`

## Level 20–30%
- Data Definition Language (DDL) Commands (`CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME`)
- Table Modifications (`ALTER TABLE ADD`, `MODIFY`, `DROP COLUMN`, `RENAME COLUMN`)
- Difference between `DROP`, `TRUNCATE`, and `DELETE`

## Level 30–40%
- Data Manipulation Language (DML) Commands (`INSERT`, `UPDATE`, `DELETE`, `MERGE`)
- Safe `UPDATE` and `DELETE` operations using explicit `WHERE` clauses
- Conditional updates using SQL `CASE` statements

## Level 40–50%
- Data Query Language (DQL): Filtering rows with `SELECT` & `WHERE`
- Operators: Comparison (`=`, `!=`), Logical (`AND`, `OR`, `NOT`), Special (`BETWEEN`, `IN`, `LIKE`, `IS NULL`)
- Wildcard pattern matching (`%` and `_`)

## Level 50–60%
- Column Sorting with `ORDER BY` (`ASC` / `DESC`) and duplicate elimination with `DISTINCT`
- Single-Row Functions: String (`UPPER`, `LOWER`, `LENGTH`, `SUBSTR`), Numeric (`ROUND`, `TRUNC`), Date (`SYSDATE`)
- `NVL` function for handling NULL mathematical calculations

## Level 60–70%
- Aggregate Functions (`COUNT(*)`, `COUNT(col)`, `SUM`, `AVG`, `MIN`, `MAX`)
- Grouping Data: `GROUP BY` clause and Group Filtering with `HAVING` clause
- SQL Query Execution Order (`FROM` → `WHERE` → `GROUP BY` → `HAVING` → `SELECT` → `ORDER BY`)

## Level 70–80%
- Database Integrity Constraints (`NOT NULL`, `UNIQUE`, `PRIMARY KEY`, `FOREIGN KEY`, `CHECK`, `DEFAULT`)
- Column-level vs Table-level constraint declarations
- Referential Integrity and `ON DELETE CASCADE`

## Level 80–90%
- SQL Joins: `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL JOIN`, `CROSS JOIN`, `SELF JOIN`
- Subqueries: Single-row, Multi-row (`IN`, `ANY`, `ALL`), Correlated Subqueries, `EXISTS`
- Set Operators: `UNION`, `INTERSECT`, `MINUS`

## Level 90–100%
- Database Objects: Views (`CREATE VIEW`), B-Tree Indexes (`CREATE INDEX`), Sequences (`NEXTVAL`, `CURRVAL`), Synonyms
- Data Control Language (DCL: `GRANT`, `REVOKE`) & Transaction Control Language (TCL: `COMMIT`, `ROLLBACK`, `SAVEPOINT`, ACID)
- SQL*Plus Formatting & Custom Report Generation (`TTITLE`, `COLUMN`, `BREAK ON`, `COMPUTE`)
- Introduction to PL/SQL Programming Blocks (`DECLARE`, `BEGIN`, `EXCEPTION`, `END;`)

---

# PRACTICAL EXERCISES

### Exercise 1: Department & Employee Query Analysis
**Question:** Display all details of salesman from Employee table whose name starts with 'K' and salary is between 10000 and 30000.  
**Required SQL command/topic:** `SELECT`, `WHERE`, `LOWER()`, `LIKE`, `BETWEEN`  
**Expected task:** Write an Oracle SQL query using relational and pattern operators.  
**Space for answer:**
```sql
-- Write your SQL query here:
SELECT * 
FROM Employee 
WHERE LOWER(Post) = 'salesman' 
  AND Emp_name LIKE 'K%' 
  AND Salary BETWEEN 10000 AND 30000;
```

---

### Exercise 2: Order Detail Report Formatting
**Question:** Create an Oracle SQL*Plus report formatting script for the `Order_detail` table displaying `Order_no`, `Order_date`, `Item`, `Item_price`, and calculate the total sum of `Item_price` at the end of the report.  
**Required SQL command/topic:** `SET PAGESIZE`, `SET LINESIZE`, `TTITLE`, `COLUMN`, `BREAK ON`, `COMPUTE SUM`  
**Expected task:** Write complete SQL*Plus report commands.  
**Space for answer:**
```sql
-- Write your SQL*Plus script here:
CLEAR COLUMNS
CLEAR BREAKS
CLEAR COMPUTES

SET PAGESIZE 30
SET LINESIZE 80

TTITLE CENTER 'ORDER DETAIL REPORT' SKIP 2

COLUMN Order_no     HEADING 'Order No'   FORMAT 999999
COLUMN Order_date   HEADING 'Order Date' FORMAT A12
COLUMN Item         HEADING 'Item Name'  FORMAT A15
COLUMN Item_price   HEADING 'Price (Rs)' FORMAT 99,99,990.00

BREAK ON REPORT
COMPUTE SUM LABEL 'TOTAL SUM:' OF Item_price ON REPORT

SELECT Order_no, TO_CHAR(Order_date, 'DD-Mon-YYYY') AS Order_date, Item, Item_price 
FROM Order_detail;
```

---

### Exercise 3: Employee & Company Subquery Filtering
**Question:** Find all details of employees who work in city "Mumbai" and do NOT work for company "InfoSystem Ltd." using a subquery.  
**Required SQL command/topic:** `SELECT`, `WHERE`, `IN` / `NOT IN`, Subquery  
**Expected task:** Write a nested SQL query.  
**Space for answer:**
```sql
-- Write your SQL query here:
SELECT * 
FROM Emp 
WHERE LOWER(city) = 'mumbai' 
  AND Emp_no NOT IN (
      SELECT Emp_no 
      FROM Emp 
      WHERE LOWER(company) = 'infosystem ltd.'
  );
```

---

### Exercise 4: Item Master Aggregation
**Question:** Calculate the average price of all items manufactured by company code 16, and display the name and price of the lowest-priced item.  
**Required SQL command/topic:** Aggregate Functions (`AVG`, `MIN`), Subquery  
**Expected task:** Write queries for average price and minimum item filtering.  
**Space for answer:**
```sql
-- Query A: Average Price
SELECT AVG(price) AS Average_Price 
FROM Item_Master 
WHERE company_code = 16;

-- Query B: Lowest Price Item Details
SELECT Item_name, price 
FROM Item_Master 
WHERE price = (SELECT MIN(price) FROM Item_Master);
```

---

### Exercise 5: Client Modification & Filtering
**Question:** Update the salary of all clients located in Surat by increasing it by 10%, and retrieve all clients who are either 'Manager' or 'Clerk'.  
**Required SQL command/topic:** `UPDATE`, `SET`, `IN`, `WHERE`  
**Expected task:** Perform update and multi-value selection.  
**Space for answer:**
```sql
-- Write your SQL queries here:
UPDATE Client 
SET salary = salary * 1.10 
WHERE LOWER(city) = 'surat';

COMMIT;

SELECT * 
FROM Client 
WHERE LOWER(post) IN ('manager', 'clerk');
```

---

### Exercise 6: Student Table Data Manipulation & Deletion
**Question:** Delete all records from the `Student` table whose age is greater than 20, or whose city is 'Jamnagar' and class is NOT 'Sem-3'.  
**Required SQL command/topic:** `DELETE FROM`, `WHERE`, `OR`, `AND`, `!=`  
**Expected task:** Delete records based on complex logical condition.  
**Space for answer:**
```sql
-- Write your SQL query here:
DELETE FROM Student 
WHERE age > 20 
   OR (LOWER(city) = 'jamnagar' AND class != 'Sem-3');

COMMIT;
```

---

### Exercise 7: Salesman Table Aggregations & Updates
**Question:** Change the city of salesman with id 8 to 'Puna', and find the maximum commission earned by any salesman situated in Mumbai, Delhi, or Puna.  
**Required SQL command/topic:** `UPDATE`, `MAX()`, `IN`  
**Expected task:** Modify record and perform aggregate calculation with filtering.  
**Space for answer:**
```sql
-- Write your SQL queries here:
UPDATE Salesman 
SET city = 'Puna' 
WHERE Sid = 8;

COMMIT;

SELECT MAX(comm) AS Max_Commission 
FROM Salesman 
WHERE LOWER(city) IN ('mumbai', 'delhi', 'puna');
```

---

### Exercise 8: Multi-Table Student Course Join Query
**Question:** Retrieve student name, course name, and age for all students aged between 23 and 27 who are enrolled in 'BCA'.  
**Required SQL command/topic:** `INNER JOIN`, `ON`, `WHERE`, `UPPER()`  
**Expected task:** Join `Student_Master` and `Course_master` tables.  
**Space for answer:**
```sql
-- Write your SQL query here:
SELECT s.sname AS Student_Name, c.c_name AS Course_Name, s.age 
FROM Student_Master s 
JOIN Course_master c ON s.c_code = c.C_code 
WHERE s.age > 23 
  AND s.age < 27 
  AND UPPER(c.c_name) = 'BCA';
```

---

# EXAM PREPARATION

## Important Definitions
1. **Primary Key:** A column or combination of columns that uniquely identifies each row in a table. It cannot contain duplicate or NULL values.
2. **Foreign Key:** A column in a table that references the Primary Key of another parent table, establishing referential integrity.
3. **Data Definition Language (DDL):** SQL commands (`CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME`) that define and modify database schema metadata. DDL auto-commits.
4. **Data Manipulation Language (DML):** SQL commands (`INSERT`, `UPDATE`, `DELETE`, `MERGE`) used to manipulate row data inside tables. DML requires `COMMIT`.
5. **View:** A virtual table defined by an underlying `SELECT` query that does not store physical data on disk.
6. **Index:** A database B-Tree search structure created on table columns to accelerate data retrieval performance.
7. **Sequence:** An Oracle database object used to generate unique, sequential numeric counter values.
8. **ACID Properties:** Transaction guarantees — Atomicity (all or nothing), Consistency (valid state), Isolation (independent execution), Durability (permanent storage).

## Important Short Questions
1. **What is the difference between CHAR and VARCHAR2 data types in Oracle?**
   - `CHAR(n)` is fixed-length (blank-pads unused space up to 2000 bytes). `VARCHAR2(n)` is variable-length (uses only actual content size up to 4000 bytes).
2. **Explain the difference between DROP, TRUNCATE, and DELETE commands.**
   - `DELETE` (DML) removes specific rows, supports rollback. `TRUNCATE` (DDL) removes all rows quickly, resets space, no rollback. `DROP` (DDL) deletes entire table schema.
3. **What is the purpose of NVL() function in Oracle?**
   - `NVL(expr1, expr2)` substitutes `expr2` if `expr1` evaluates to NULL, preventing math calculation errors on NULL columns.
4. **Differentiate between WHERE clause and HAVING clause.**
   - `WHERE` filters individual rows before grouping (cannot use aggregates). `HAVING` filters group summary results after `GROUP BY` (allows aggregates).
5. **What is a Pseudo-column? Give two examples in Oracle.**
   - Pseudo-columns behave like table columns but are managed internally by Oracle. Examples: `ROWNUM` (row position index) and `ROWID` (physical disk storage address).

## Important Long Questions
1. **Explain Database Integrity Constraints in Oracle SQL with syntax and examples.**
   - Detail `NOT NULL`, `UNIQUE`, `PRIMARY KEY`, `FOREIGN KEY`, `CHECK`, and `DEFAULT` with column-level and table-level syntax examples.
2. **Discuss various types of SQL Joins with Venn diagrams and syntax.**
   - Cover `INNER JOIN`, `LEFT OUTER JOIN`, `RIGHT OUTER JOIN`, `FULL OUTER JOIN`, `CROSS JOIN`, and `SELF JOIN`.
3. **What is PL/SQL? Explain the block structure of PL/SQL with an example anonymous block.**
   - Explain `DECLARE`, `BEGIN`, `EXCEPTION`, and `END;` blocks alongside `%TYPE` variable declarations and exception handling logic.
4. **Explain SQL*Plus formatting commands for generating customized business reports.**
   - Explain `SET PAGESIZE`, `SET LINESIZE`, `TTITLE`, `COLUMN`, `BREAK ON`, and `COMPUTE SUM` commands with a full report script.

## Important SQL Programs/Queries
1. **Creating linked parent-child tables with Foreign Key constraints:**
   ```sql
   CREATE TABLE Department (
       Dept_no NUMBER(3) PRIMARY KEY,
       Depart_Name VARCHAR2(30) NOT NULL
   );

   CREATE TABLE Employee (
       Emp_id NUMBER(6) PRIMARY KEY,
       Emp_name VARCHAR2(50) NOT NULL,
       Dept_id NUMBER(3),
       CONSTRAINT fk_dept FOREIGN KEY (Dept_id) REFERENCES Department(Dept_no) ON DELETE CASCADE
   );
   ```

2. **Calculating employee salary components with NVL:**
   ```sql
   SELECT e.emp_name, d.dept_name, 
          (s.sal + NVL(s.hra, 0) + NVL(s.ma, 0) - NVL(s.pf, 0)) AS Net_Salary 
   FROM Emp_mast e 
   JOIN Dept_mast d ON e.dept_code = d.Dept_no 
   JOIN Salary_mast s ON e.Emp_no = s.Emp_no;
   ```

## Viva Questions
1. **Q:** Can a Primary Key column accept NULL values?  
   **A:** No. A Primary Key strictly enforces both `UNIQUE` and `NOT NULL` rules.
2. **Q:** What is the result of `NUMBER + NULL` in SQL?  
   **A:** `NULL`. Any arithmetic operation involving NULL results in NULL.
3. **Q:** Which table in Oracle is used to select system date or evaluate math expressions?  
   **A:** The `DUAL` table (`SELECT SYSDATE FROM DUAL;`).
4. **Q:** Does DDL require executing a COMMIT command?  
   **A:** No. DDL commands auto-commit immediately upon execution.
5. **Q:** What is the default sorting order of `ORDER BY`?  
   **A:** Ascending (`ASC`).

## MCQs
1. Which command is used to remove all rows from a table quickly without logging individual row deletions?  
   a) DELETE  
   b) REMOVE  
   c) **TRUNCATE**  
   d) DROP  
   *Answer:* c) TRUNCATE

2. Which SQL clause is used to filter aggregated group results?  
   a) WHERE  
   b) **HAVING**  
   c) GROUP BY  
   d) ORDER BY  
   *Answer:* b) HAVING

3. In Oracle SQL, which data type is variable-length character string?  
   a) CHAR  
   b) **VARCHAR2**  
   c) LONG CHAR  
   d) TEXT  
   *Answer:* b) VARCHAR2

4. Which wildcard character represents exactly one single character in `LIKE` pattern matching?  
   a) `%`  
   b) `*`  
   c) **`_`**  
   d) `?`  
   *Answer:* c) `_`

5. Which command saves pending transaction modifications permanently?  
   a) SAVEPOINT  
   b) ROLLBACK  
   c) **COMMIT**  
   d) GRANT  
   *Answer:* c) COMMIT

---

# COMMON SQL ERRORS

| Wrong | Correct | Reason |
| :--- | :--- | :--- |
| `FORM` | `FROM` | Keyword misspelling (`FROM` specifies target table). |
| `creact` | `CREATE` | Incorrect keyword spelling. |
| `WHERE SUM(sal) > 5000` | `HAVING SUM(sal) > 5000` | Aggregate functions are NOT allowed in `WHERE`; use `HAVING`. |
| `sal = NULL` | `sal IS NULL` | NULL values cannot be checked with `=` operator; use `IS NULL`. |
| `UPDATE Student city = 'Surat';` | `UPDATE Student SET city = 'Surat';` | Missing required `SET` keyword in `UPDATE` statement. |
| `INSERT Student VALUES (...)` | `INSERT INTO Student VALUES (...)` | Missing required `INTO` keyword in `INSERT` statement. |
| `DELETE * FROM Student;` | `DELETE FROM Student;` | `DELETE` takes no `*` parameter; syntax is `DELETE FROM table`. |
| `VARCHAR` in Oracle | `VARCHAR2` | Oracle standard requires `VARCHAR2` for variable character data. |
| `'18-11-1990'` directly into DATE | `TO_DATE('18-11-1990', 'DD-MM-YYYY')` | Custom string date format requires explicit `TO_DATE` conversion. |
| `SELECT name GROUP BY city;` | `SELECT city, COUNT(name) FROM students GROUP BY city;` | Columns in `SELECT` must either be aggregated or listed in `GROUP BY`. |

---

# FINAL REVISION SHEET

### Important SQL Commands Summary
- `CREATE`: Creates table/object schema (DDL, Auto-commit).
- `ALTER`: Adds/Modifies/Drops columns in table structure (DDL, Auto-commit).
- `DROP`: Deletes entire table and data permanently (DDL, Auto-commit).
- `TRUNCATE`: Fast wipe of all table rows; deallocates storage space (DDL, Auto-commit).
- `INSERT`: Adds new rows into table (DML, Needs `COMMIT`).
- `UPDATE`: Modifies existing row values (DML, Needs `COMMIT`, Use `WHERE`).
- `DELETE`: Removes specific or all rows (DML, Needs `COMMIT`, Supports rollback).
- `SELECT`: Retrieves data rows from table (DQL).
- `GRANT` / `REVOKE`: Manages database user permissions (DCL).
- `COMMIT` / `ROLLBACK` / `SAVEPOINT`: Manages transaction integrity (TCL).

### Key Definitions to Remember
- **Primary Key:** Unique + NOT NULL column uniquely identifying each row.
- **Foreign Key:** Linkage referencing Primary Key of parent table.
- **View:** Virtual table defined by a `SELECT` query.
- **Index:** B-Tree structure accelerating query search speed.
- **Sequence:** Numeric counter generating sequential Primary Key IDs.

### Crucial Oracle & SQL*Plus Highlights
- Oracle string data type: Use `VARCHAR2`.
- Custom date insertion: Always wrap string dates with `TO_DATE('str', 'format')`.
- Dual table: `SELECT ... FROM DUAL;` for evaluating expressions.
- SQL*Plus Formatting: `SET PAGESIZE 30`, `SET LINESIZE 80`, `TTITLE`, `COLUMN col FORMAT 99,99,990.00`, `BREAK ON REPORT`, `COMPUTE SUM`.

### Top Exam Topics for BCA Semester 3
1. DDL vs DML Detailed Difference Table
2. DROP vs TRUNCATE vs DELETE Comparison
3. Column-level vs Table-level Constraints (`PRIMARY KEY`, `FOREIGN KEY`, `CHECK`)
4. SQL Joins (`INNER`, `LEFT`, `RIGHT`, `FULL`) & Subqueries (`IN`, `EXISTS`)
5. Transaction ACID Properties & TCL Commands (`COMMIT`, `ROLLBACK`, `SAVEPOINT`)
6. PL/SQL Block Architecture (`DECLARE`, `BEGIN`, `EXCEPTION`, `END;`)
