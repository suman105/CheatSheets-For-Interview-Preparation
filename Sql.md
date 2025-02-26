# SQL Overview

SQL (Structured Query Language) is a standard language for managing and manipulating relational databases. It is used to perform various operations such as querying data, updating data, inserting data, and managing database structures. Below is a comprehensive overview of SQL.

## Basic SQL Commands
- **SELECT**: Retrieves data from a database.
  ```sh
  SELECT * FROM employees;
- **INSERT INTO**: Inserts new data into a database table.
  ```sh
  INSERT INTO employees (name, age, department) VALUES ('John Doe', 30, 'HR');
    
- **UPDATE**: Updates existing data within a table.
  ```sh
  UPDATE employees SET age = 31 WHERE name = 'John Doe';
    
- **DELETE**: Deletes data from a table.
  ```sh
  DELETE FROM employees WHERE name = 'John Doe';

## Filtering Data
- **WHERE**: Filters records based on specified conditions.
  ```sh
  SELECT * FROM employees WHERE department = 'HR';
- **AND, OR, NOT**: Logical operators to combine conditions.
  ```sh
  SELECT * FROM employees WHERE department = 'HR' AND age > 25;
- **IN**: Checks if a value is within a set of values.
  ```sh
  SELECT * FROM employees WHERE department IN ('HR', 'Finance');
- **BETWEEN**: Filters records within a range.
  ```sh
  SELECT * FROM employees WHERE age BETWEEN 25 AND 35;
- **LIKE**: Filters records using pattern matching.
  ```sh
  SELECT * FROM employees WHERE name LIKE 'J%';
- **IS NULL, IS NOT NULL**: Checks for null values.
  ```sh
  SELECT * FROM employees WHERE department IS NULL;
- **EXISTS**: Checks if a subquery returns any rows.
  ```sh
  SELECT * FROM employees WHERE EXISTS (SELECT 1 FROM departments WHERE departments.id = employees.department_id);
  
# Sorting and Limiting Data
- **ORDER BY**: Sorts the result set in ascending or descending order.
  ```sh
  SELECT * FROM employees ORDER BY age DESC;
- **LIMIT**: Limits the number of records returned.
  ```sh
  SELECT * FROM employees LIMIT 5;
- **DISTINCT**: Selects unique records.
  ```sh
  SELECT DISTINCT department FROM employees;

## Aggregating Data
- **COUNT()**: Returns the number of rows.
  ```sh
  SELECT COUNT(*) FROM employees;
- **SUM()**: Returns the sum of a numeric column.
  ```sh
  SELECT SUM(salary) FROM employees;
- **AVG()**: Returns the average value of a numeric column.
  ```sh
  SELECT AVG(age) FROM employees;
- **MIN()**: Returns the minimum value of a column.
  ```sh
  SELECT MIN(age) FROM employees;
- **MAX()**: Returns the maximum value of a column.
  ```sh
  SELECT MAX(age) FROM employees;
- **GROUP BY**: Groups rows that have the same values into summary rows.
  ```sh
  SELECT department, COUNT(*) FROM employees GROUP BY department;
- **HAVING**: Filters groups based on a condition.
```sh
SELECT department, COUNT(*) FROM employees GROUP BY department HAVING COUNT(*) > 5;
```

## Joins
- **INNER JOIN**: Returns records with matching values in both tables.
- **LEFT JOIN (LEFT OUTER JOIN)**: Returns all records from the left table and matched records from the right table.
- **RIGHT JOIN (RIGHT OUTER JOIN)**: Returns all records from the right table and matched records from the left table.
- **FULL JOIN (FULL OUTER JOIN)**: Returns all records when there is a match in either left or right table.
- **CROSS JOIN**: Returns the Cartesian product of the two tables.
- **SELF JOIN**: Joins a table to itself.

## Subqueries
- **Subqueries in SELECT**: Subquery within a SELECT statement.
- **Subqueries in WHERE**: Subquery within a WHERE clause.
- **Subqueries in FROM**: Subquery within a FROM clause.

## Set Operations
- **UNION**: Combines the result sets of two SELECT statements (removes duplicates).
- **UNION ALL**: Combines the result sets of two SELECT statements (includes duplicates).
- **INTERSECT**: Returns common records from two SELECT statements.
- **EXCEPT**: Returns records from the first SELECT statement that are not in the second.

## Data Modification
- **INSERT**: Adds new rows to a table.
- **UPDATE**: Modifies existing rows in a table.
- **DELETE**: Removes rows from a table.

## Indexing
- **CREATE INDEX**: Creates an index on a table.
- **DROP INDEX**: Drops an index from a table.
- **UNIQUE INDEX**: Ensures all values in the index are unique.
- **FULL-TEXT INDEX**: Used for full-text searches.
- **COMPOSITE INDEX**: Index on multiple columns.

## Transactions
- **BEGIN TRANSACTION**: Starts a transaction.
- **COMMIT**: Commits the current transaction.
- **ROLLBACK**: Rolls back the current transaction.
- **SAVEPOINT**: Sets a savepoint within a transaction.
- **SET TRANSACTION ISOLATION LEVEL**: Sets the isolation level for the transaction.

## Views
- **CREATE VIEW**: Creates a virtual table based on the result set of a SQL statement.
- **DROP VIEW**: Deletes a view.
- **ALTER VIEW**: Modifies a view.
- **INSERT INTO VIEW**: Inserts data into a view.
- **UPDATE VIEW**: Updates data in a view.

## Triggers
- **CREATE TRIGGER**: Creates a trigger that is executed when a specified event occurs.
- **DROP TRIGGER**: Deletes a trigger.
- **AFTER INSERT/UPDATE/DELETE**: Trigger executed after the specified event.
- **BEFORE INSERT/UPDATE/DELETE**: Trigger executed before the specified event.

## Common Table Expressions (CTEs)
- **WITH CTE AS**: Defines a temporary result set that can be referenced within a SELECT, INSERT, UPDATE, or DELETE statement.
- **RECURSIVE CTE**: A CTE that references itself.
- **WITH TEMPORARY CTE**: A temporary CTE.

## Window Functions
- **ROW_NUMBER()**: Assigns a unique number to each row.
- **RANK()**: Assigns a rank to each row within a partition.
- **DENSE_RANK()**: Assigns a rank to each row within a partition without gaps.
- **NTILE()**: Distributes rows into a specified number of groups.
- **LEAD()**: Accesses data from a subsequent row.
- **LAG()**: Accesses data from a previous row.
- **FIRST_VALUE()**: Returns the first value in an ordered set of values.
- **LAST_VALUE()**: Returns the last value in an ordered set of values.
- **SUM() OVER()**: Calculates a cumulative sum.
- **AVG() OVER()**: Calculates a cumulative average.
- **PARTITION BY**: Divides the result set into partitions.
- **ORDER BY (WITHIN WINDOW FUNCTIONS)**: Orders rows within partitions.

## Date and Time Functions
- **GETDATE()**: Returns the current date and time.
- **CURRENT_TIMESTAMP**: Returns the current date and time.
- **DATEADD()**: Adds a specified time interval to a date.
- **DATEDIFF()**: Returns the difference between two dates.
- **DATEPART()**: Returns a specified part of a date.
- **DATE_FORMAT()**: Formats a date.
- **NOW()**: Returns the current date and time.
- **EXTRACT()**: Extracts a part of a date.
- **TIMESTAMPDIFF()**: Returns the difference between two timestamps.

## Conditional Logic
- **CASE WHEN**: Performs conditional logic in SQL.
- **IFNULL()**: Returns a specified value if the expression is NULL.
- **COALESCE()**: Returns the first non-null value in a list.

---

This comprehensive overview covers the essential aspects of SQL, including basic commands, filtering, sorting, aggregating data, joins, subqueries, set operations, data modification, indexing, transactions, views, triggers, CTEs, window functions, date and time functions, and conditional logic. Mastering these concepts will enable you to effectively manage and manipulate relational databases.
