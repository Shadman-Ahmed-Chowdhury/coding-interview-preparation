# SQL Learning Notes
This directory contains my comprehensive notes and learning resources on SQL (Structured Query Language). It covers fundamental concepts, advanced topics, and practical examples to help you master SQL for database management and data manipulation.

## 📚 Contents
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


