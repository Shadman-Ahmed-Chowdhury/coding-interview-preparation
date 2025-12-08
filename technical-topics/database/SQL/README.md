# SQL Learning Notes
This directory contains my comprehensive notes and learning resources on SQL (Structured Query Language). It covers fundamental concepts, advanced topics, and practical examples to help you master SQL for database management and data manipulation.

## Contents
- [Before Getting Started](#before-getting-started)
- [SQL Basics](#sql-basics)
    - [What is SQL?](#what-is-sql)
    - [Key SQL Commands](#key-sql-commands)
    - [SQL Key Words](#sql-key-words)
- [Data Definition Language (DDL)](#data-definition-language-ddl)
    - [Common DDL Commands](#common-ddl-commands)
- [Data Manipulation Language (DML)](#data-manipulation-language-dml)
    - [Common DML Commands](#common-dml-commands)
- [AGGREGATE Queries](#aggregate-queries)
- [Data Constraints](#data-constraints)
- [JOIN Queries](#join-queries)
- [Subqueries](#subqueries)
    - [Corelated Subquery](#corelated-subquery)
- [Advanced Functions](#advanced-functions)
    - [String Functions](#string-functions)
    - [Date and Time Functions](#date-and-time-functions)
    - [Numeric Functions](#numeric-functions)
    - [Conditional Functions](#conditional-functions)
- [Views](#views)   
    - [Creating Views](#creating-views)
    - [Modifying Views](#modifying-views)
    - [Dropping Views](#dropping-views)
- [Transactions](#transactions)
    - [ACID Properties](#acid-properties)
    - [BEGIN, COMMIT, ROLLBACK, SAVEPOINT](#begin-commit-rollback-savepoint)
- [Query Optimization Tips](#query-optimization-tips)
- [Indexes](#indexes)
    - [Creating Indexes](#creating-indexes)
    - [Dropping Indexes](#dropping-indexes)
    - [Query Optimization Tips](#query-optimization-tips)
    - [Managing Indexes](#managing-indexes)
    - [Indexes Notes](#indexes-notes)
- [Normalization](#normalization)
    - [Normal Forms](#normal-forms) 


## Before Getting Started
### Relation Databases
- A relational database is a type of database that stores and provides access to data points that are related to one another. Data in a relational database is organized into tables (also known as relations), which consist of rows and columns.
- Each table represents a specific entity (e.g., customers, orders, products) and contains records (rows) that hold data about that entity.
- Tables can be linked to one another through relationships, allowing for complex queries and data retrieval across multiple tables.

### Benefits of Relational Databases
- **Structured Data**: Data is organized in a structured manner using tables, making it easy to understand and manage.
- **Data Integrity**: Relational databases enforce data integrity through constraints, ensuring that data remains accurate and consistent. (ACID properties: Atomicity, Consistency, Isolation, Durability)
- **Flexibility**: SQL allows for complex queries and data manipulation, enabling users to retrieve and analyze data in various ways.
- **Scalability**: Relational databases can handle large volumes of data and support multiple users simultaneously.
- **Security**: Relational databases provide robust security features to protect sensitive data.
### Limitations of Relational Databases
- **Complexity**: Designing and managing relational databases can be complex, especially for large-scale applications.
- **Performance**: For certain types of applications (e.g., those requiring high-speed read/write operations), relational databases may not perform as well as NoSQL databases.
- **Schema Rigidity**: Changes to the database schema can be challenging and may require significant effort, especially in production environments.
- **Scalability Challenges**: While relational databases can scale vertically (by adding more resources to a single server), horizontal scaling (distributing data across multiple servers) can be more complex compared to NoSQL databases.

### SQL vs NoSQL
| Feature               | SQL Databases                              | NoSQL Databases                           |
|-----------------------|--------------------------------------------|-------------------------------------------|
| Data Model            | Relational (tables with rows and columns)  | Non-relational (document, key-value, graph, column) |
| Schema                | Fixed schema (predefined structure)          | Flexible schema (dynamic structure)      |
| Scalability           | Vertical scaling (adding resources to a single server) | Horizontal scaling (distributing data across multiple servers) |
| Query Language       | SQL (Structured Query Language)            | Varies (e.g., JSON queries, graph queries) |
| Transactions         | ACID compliance (Atomicity, Consistency, Isolation, Durability) | Varies (some support ACID, others eventual consistency) |
| Use Cases            | Complex queries, structured data, transactions | Big data, real-time applications, unstructured data |

## SQL Basics
### What is SQL?
SQL (Structured Query Language) is a standardized programming language used to manage and manipulate relational databases. It allows users to perform various operations such as querying data, inserting records, updating existing data, and deleting records.
[Back To Top ⬆️](#contents)

### Key SQL Commands
- **SELECT**: Retrieve data from one or more tables.
- **INSERT**: Add new records to a table.
- **UPDATE**: Modify existing records in a table.
- **DELETE**: Remove records from a table.
- **CREATE**: Create new database objects such as tables, indexes, and views.
- **ALTER**: Modify the structure of existing database objects.
- **DROP**: Delete database objects such as tables and indexes. 

[Back To Top ⬆️](#contents)

### SQL Key Words
| Keyword      | Description                                      |
|--------------|--------------------------------------------------|
| SELECT       | Retrieve data from a database table              |
| FROM         | Specify the table to retrieve data from          |
| WHERE        | Filter records based on specified conditions     |
| INSERT INTO  | Add new records to a table                       |
| VALUES       | Specify the values to be inserted into a table   |
| UPDATE       | Modify existing records in a table               |
| SET          | Specify the columns and values to be updated     |
| DELETE       | Remove records from a table                      |
| CREATE TABLE | Create a new table in the database               |
| ALTER TABLE  | Modify the structure of an existing table        |
| DROP TABLE   | Delete a table from the database                 |
| JOIN         | Combine rows from two or more tables based on a related column |
| ORDER BY     | Sort the result set in ascending or descending order |
| GROUP BY     | Group rows that have the same values in specified columns |
| HAVING       | Filter groups based on specified conditions      |
| DISTINCT     | Retrieve unique values from a column             |

[Back To Top ⬆️](#contents)

## Data Definition Language (DDL)
- Data Definition Language (DDL) is a subset of SQL that deals with the creation, modification, and deletion of database objects such as tables, indexes, and views.

[Back To Top ⬆️](#contents)

### Common DDL Commands
- **CREATE**: Used to create new database objects.
  ```sql
  CREATE TABLE Employees (
      EmployeeID INT PRIMARY KEY,
      FirstName VARCHAR(50),
      LastName VARCHAR(50),
      HireDate DATE
  );
  ```
- **ALTER**: Used to modify the structure of existing database objects.
  ```sql
  ALTER TABLE Employees
  ADD COLUMN Email VARCHAR(100);    
  ```
- **DROP**: Used to delete database objects.
  ```sql
    DROP TABLE Employees;
    ```
- **TRUNCATE**: Used to remove all records from a table, but keeps the table structure intact.
  ```sql
  TRUNCATE TABLE Employees;
  ```

[Back To Top ⬆️](#contents)

## Data Manipulation Language (DML)
- Data Manipulation Language (DML) is a subset of SQL that deals with the manipulation of data within database tables.

[Back To Top ⬆️](#contents)

### Common DML Commands
- **SELECT**: Used to retrieve data from one or more tables.
```sql
SELECT FirstName, LastName FROM Employees WHERE HireDate > '2020-01-01';
```
- **INSERT**: Used to add new records to a table.
```sql
INSERT INTO Employees (EmployeeID, FirstName, LastName, HireDate)
VALUES (1, 'John', 'Doe', '2021-06-15');
```
- **UPDATE**: Used to modify existing records in a table.
```sql
UPDATE Employees
SET Email = 'john.doe@example.com'
WHERE EmployeeID = 1;
```
- **DELETE**: Used to remove records from a table.
```sql
DELETE FROM Employees
WHERE EmployeeID = 1;
```

[Back To Top ⬆️](#contents)

### AGGREGATE Queries
- Aggregate functions perform calculations on a set of values and return a single value.

| Function       | Description                                      |
|----------------|--------------------------------------------------|
| COUNT          | Returns the number of rows that match a specified condition |
| SUM            | Returns the total sum of a numeric column         |
| AVG            | Returns the average value of a numeric column     |
| MIN            | Returns the smallest value in a column           |
| MAX            | Returns the largest value in a column            |
| GROUP BY      | Groups rows that have the same values in specified columns into summary rows |
| HAVING        | Filters groups based on a specified condition     |

Example:
```sql
SELECT COUNT(EmployeeID) AS TotalEmployees, Department
FROM Employees
GROUP BY Department;
```

[Back To Top ⬆️](#contents)

## Data Constraints
- Data constraints are rules applied to database columns to ensure data integrity and consistency.

| Constraint        | Description                                      |
|-------------------|--------------------------------------------------|
| PRIMARY KEY       | Uniquely identifies each record in a table       |
| FOREIGN KEY       | Ensures referential integrity between tables     |
| NOT NULL          | Ensures that a column cannot have a NULL value   |
| UNIQUE            | Ensures that all values in a column are unique   |
| NOT NULL          | Ensures that a column cannot have a NULL value   |
| CHECK             | Ensures that values in a column meet a specific condition |
Example:
```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    Email VARCHAR(100) UNIQUE,
    HireDate DATE CHECK (HireDate >= '2000-01-01')
);
```
[Back To Top ⬆️](#contents)

## JOIN Queries
- JOIN operations are used to combine rows from two or more tables based on a related column between them.

| JOIN Type        | Description                                      |
|------------------|--------------------------------------------------|
| INNER JOIN       | Returns records that have matching values in both tables |
| LEFT JOIN        | Returns all records from the left table and matched records from the right table |
| RIGHT JOIN       | Returns all records from the right table and matched records from the left table |
| FULL JOIN        | Returns all records when there is a match in either left or right table |
| CROSS JOIN       | Returns the Cartesian product of both tables     |
| Self JOIN        | Joins a table with itself to compare rows within the same table |

Example of INNER JOIN:
```sql
SELECT Employees.FirstName, Employees.LastName, Departments.DepartmentName
FROM Employees
INNER JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
```

Example of LEFT JOIN:
```sql
SELECT Employees.FirstName, Employees.LastName, Departments.DepartmentName
FROM Employees
LEFT JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
```

[Back To Top ⬆️](#contents)

## Subqueries
- A subquery is a query nested inside another query. It can be used in SELECT, INSERT, UPDATE, or DELETE statements to perform operations based on the results of another query.

Example of a Subquery:
```sql
SELECT FirstName, LastName
FROM Employees
WHERE DepartmentID IN (SELECT DepartmentID FROM Departments WHERE Location = 'New York');
```

[Back To Top ⬆️](#contents)

### Corelated Subquery
- A correlated subquery is a subquery that references columns from the outer query. It is executed once for each row processed by the outer query.

Example of a Correlated Subquery:
```sql
SELECT E1.FirstName, E1.LastName
FROM Employees E1
WHERE E1.Salary > (SELECT AVG(E2.Salary) FROM Employees E2 WHERE E2.DepartmentID = E1.DepartmentID);
```

[Back To Top ⬆️](#contents)

## Advanced Functions
- SQL provides various advanced functions to perform complex operations on data.

### String Functions
| Function       | Description                                      |
|----------------|--------------------------------------------------|
| CONCAT         | Combines two or more strings into one            |
| SUBSTRING      | Extracts a substring from a string                |
| LENGTH         | Returns the length of a string                    |
Example:
```sql
SELECT CONCAT(FirstName, ' ', LastName) AS FullName
FROM Employees;
```
[Back To Top ⬆️](#contents)

### Date and Time Functions

| Function       | Description                                      |
|----------------|--------------------------------------------------|
| NOW()          | Returns the current date and time                 |
| DATEADD        | Adds a specified time interval to a date          |
| DATEDIFF       | Returns the difference between two dates          |
| DATEPART      | Returns a specific part of a date (e.g., year, month, day) |
| TIME          | Returns the time portion of a datetime value       |
| TIMESTAMP    | Returns the timestamp portion of a datetime value  |
Example:
```sql
SELECT FirstName, LastName, HireDate, DATEDIFF(NOW(), HireDate)
AS DaysEmployed
FROM Employees;
``` 
[Back To Top ⬆️](#contents)

### Numeric Functions
| Function       | Description                                      |
|----------------|--------------------------------------------------|
| ROUND          | Rounds a numeric value to a specified number of decimal places |
| CEIL           | Rounds a numeric value up to the nearest integer  |
| FLOOR          | Rounds a numeric value down to the nearest integer|
| ABS            | Returns the absolute value of a numeric expression|
Example:
```sql
SELECT FirstName, LastName, Salary, ROUND(Salary, 2) AS RoundedSalary
FROM Employees;
```
[Back To Top ⬆️](#contents)

### Conditional Functions
| Function       | Description                                      |
|----------------|--------------------------------------------------|
| CASE           | Performs conditional logic in SQL queries        |
| NULLIF         | Returns NULL if two expressions are equal        |
| COALESCE       | Returns the first non-NULL expression from a list|
Example:
```sql
SELECT FirstName, LastName,
CASE
    WHEN Salary < 50000 THEN 'Low'
    WHEN Salary BETWEEN 50000 AND 100000 THEN 'Medium'
    ELSE 'High'
END AS SalaryRange
FROM Employees;
```
[Back To Top ⬆️](#contents)


## Views
- A view is a virtual table that is based on the result set of a SQL query. It provides a way to simplify complex queries, and present data in a specific format.

### Creating Views
```sql
CREATE VIEW EmployeeView AS
SELECT FirstName, LastName, DepartmentID
FROM Employees
JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID
WHERE HireDate > '2020-01-01';
```
[Back To Top ⬆️](#contents)
### Modifying Views
```sql
CREATE OR REPLACE VIEW EmployeeView AS
SELECT FirstName, LastName, DepartmentID, Email
FROM Employees
JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID
WHERE HireDate > '2020-01-01';
```
[Back To Top ⬆️](#contents)

### Dropping Views

```sql
DROP VIEW EmployeeView;
```
[Back To Top ⬆️](#contents) 


## Transactions
- A transaction is a sequence of one or more SQL operations that are executed as a single unit of work. Transactions ensure data integrity and consistency by adhering to the ACID properties (Atomicity, Consistency, Isolation, Durability).

### ACID Properties
- **Atomicity**: Ensures that all operations within a transaction are completed successfully. If any operation fails, the entire transaction is rolled back.
- **Consistency**: Ensures that a transaction brings the database from one valid state to another valid state, maintaining data integrity.
- **Isolation**: Ensures that concurrent transactions do not interfere with each other, maintaining data consistency.
- **Durability**: Ensures that once a transaction is committed, its changes are permanent and will survive system failures.

### BEGIN, COMMIT, ROLLBACK, SAVEPOINT
- **BEGIN**: Starts a new transaction. 
- **COMMIT**: Saves all changes made during the transaction to the database.
- **ROLLBACK**: Undoes all changes made during the transaction, reverting the database to its previous state.
- **SAVEPOINT**: Sets a point within a transaction to which you can later roll back

[Back To Top ⬆️](#contents)

## Query Optimization Tips
Some general optimization tips include:
- Select only the columns you need instead of using SELECT *.
- Use LIMIT to preview query results when appropriate.
- Use wildcards(%) only at the end of a phrase.
- Avoid select distinct unless necessary.
- Run large queries during off-peak hours.

[Back To Top ⬆️](#contents)

## Indexes
- An index is a database object that improves the speed of data retrieval operations on a table at the cost of additional storage space and slower write operations. Indexes are created on one or more columns of a table.

### Creating Indexes
```sql
CREATE INDEX idx_lastname ON Employees (LastName);
```
### Dropping Indexes
```sql
DROP INDEX idx_lastname;
```
[Back To Top ⬆️](#contents)

### Query Optimization Tips
- Use indexes on columns that are frequently used in WHERE clauses and JOIN conditions.
- Avoid using SELECT *; instead, specify only the columns you need.
- Use EXPLAIN to analyze query execution plans and identify performance bottlenecks.
[Back To Top ⬆️](#contents)

### Managing Indexes
- Regularly monitor and maintain indexes to ensure optimal performance.
- Rebuild or reorganize indexes as needed to reduce fragmentation.
- Consider the trade-offs between read and write performance when creating indexes.
```sql
ALTER INDEX idx_lastname REBUILD;
```

```sql
ALTER INDEX idx_lastname REORGANIZE;
``` 

### Indexes Notes:
🔹 What is an Index?

A database index is like a phonebook.
Instead of checking every row (sequential scan), the DB uses a sorted structure to jump directly to the relevant data.

👉 Goal: Faster searches, faster filtering, faster sorting.

🔹 Types of Index Structures
1. B-Tree Index (Most common)

Default index type in almost all databases.
Great for:
Exact matches (WHERE id = 5)
Range queries (WHERE amount > 100)
Sorting operations (ORDER BY created_at)

2. LSM Tree Index

Mostly used in write-heavy systems (e.g., Cassandra, RocksDB).
Writes = extremely fast
Reads might be slower compared to B-Tree.

🔹 Primary Key Index
Every table’s PRIMARY KEY automatically gets a B-Tree index.
Example:
```sql
CREATE TABLE employees (
  id SERIAL PRIMARY KEY,
  name TEXT
);
```
The id column automatically has a B-Tree index.

#### 📊 EXPLAIN ANALYZE Examples (Corrected Notes)
✅ 1. Search using Primary Key
```sql
EXPLAIN ANALYZE 
SELECT id FROM employees WHERE id = 200;
```

Expected result:
- Index Only Scan (because PostgreSQL can get all required columns from the index itself)
- Heap Fetches = 0 (no need to touch table pages)
- Very fast!

Example output:
- Index Only Scan
- Heap Fetches: 0
- Execution time: 0.084 ms

⚠️ 2. Using an Index Scan but reading non-indexed columns
EXPLAIN ANALYZE
SELECT name FROM employees WHERE id = 5000;


Here:

Filter uses indexed column (id)

But name is not in the index, so PostgreSQL must go to the table (heap)

Result:

Index Scan on employees
Execution time: ~2.5 ms


🔸 This is slower than an Index Only Scan because heap lookups take time.

❌ 3. Searching by a non-indexed column
EXPLAIN ANALYZE
SELECT id, name FROM employees WHERE name = 'SH';


Since name is not indexed, PostgreSQL must scan the whole table.

Because the table is huge, PostgreSQL chooses a Parallel Seq Scan.

Result:

Workers: 2
Parallel Seq Scan
Execution time: ~3113 ms


🔥 This is VERY SLOW compared to index scans.

❌ Worst-Case Pattern: LIKE %...%
SELECT * FROM employees WHERE name LIKE '%sh%';


PostgreSQL cannot use B-Tree index for patterns starting with %

Full Sequential Scan → slowest possible

🚀 Creating an Index to Speed Up Name Search
CREATE INDEX idx_employee_name ON employees(name);


Now run:

EXPLAIN ANALYZE
SELECT id, name FROM employees WHERE name = 'SH';


Result:

Index Scan using idx_employee_name
Execution time: ~47 ms


🔸 Dramatic improvement from 3113 ms → 47 ms
This is the power of indexing correctly.

📌 Additional Important Notes
Index Only Scan vs Index Scan vs Seq Scan
Type	When used	Fast?
Index Only Scan	All requested columns exist inside index	⭐ Fastest
Index Scan	Uses index but must fetch extra columns from heap	⭐⭐ Fast
Seq Scan / Parallel Seq Scan	No useful index exists	❌ Slowest
🔸 When NOT to Use Indexes

Indexes slow down:

INSERT

UPDATE

DELETE

Because indexes must also be updated.

Don't index:

Very small tables

Columns with low cardinality (e.g., gender = 'M/F')

Columns frequently updated

🔸 Index Best Practices

Index columns used in WHERE and JOIN

Avoid indexing frequently updated columns

Composite indexes should follow filtering order:

CREATE INDEX idx ON employees (department_id, name);


For text search or LIKE '%word%':
Use GIN index with pg_trgm:
```sql
CREATE EXTENSION pg_trgm;
CREATE INDEX idx_trgm_name ON employees USING gin(name gin_trgm_ops);
```

[Back To Top ⬆️](#contents)

## Normalization
- Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity. It involves dividing large tables into smaller, related tables and defining relationships between them.

### Normal Forms
- **First Normal Form (1NF)**: 
Ensures that each column contains atomic values and each record is unique.
- **Second Normal Form (2NF)**:
Ensures that all non-key attributes are fully functionally dependent on the primary key.
- **Third Normal Form (3NF)**:
Ensures that all non-key attributes are not transitively dependent on the primary key.
- **Boyce-Codd Normal Form (BCNF)**:
A stricter version of 3NF that handles certain types of anomalies.

Example of Normalization:
Consider a table storing employee information:
| EmployeeID | Name       | Department  | Manager    |
|------------|------------|-------------|------------|
| 1          | John Doe   | Sales       | Jane Smith |
| 2          | Alice Brown| Marketing   | Bob Johnson |

To normalize this table to 3NF, we can create two separate tables:

**Employees Table**:
| EmployeeID | Name       | DepartmentID |
|------------|------------|--------------|
| 1          | John Doe   | 1            |
| 2          | Alice Brown| 2            |

**Departments Table**:
| DepartmentID | Department  | Manager    |
|--------------|-------------|------------|
| 1            | Sales       | Jane Smith |
| 2            | Marketing   | Bob Johnson |

This structure reduces redundancy and ensures data integrity.
[Back To Top ⬆️](#contents)

