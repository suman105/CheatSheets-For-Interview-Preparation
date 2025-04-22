# SQL Overview

- SQL (Structured Query Language) is a standard language for managing and manipulating relational databases. It is used to perform various operations such as querying data, updating data, inserting data, and managing database structures. Below is a comprehensive overview of SQL.

- If you want to see the Solutions for the **[LeetCode SQL 50](https://github.com/suman105/LeetCode-SQL-50)**

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
  ```sh
  SELECT employees.name, departments.name 
  FROM employees 
  INNER JOIN departments ON employees.department_id = departments.id;
- **LEFT JOIN (LEFT OUTER JOIN)**: Returns all records from the left table and matched records from the right table.
  ```sh
  SELECT employees.name, departments.name 
  FROM employees 
  LEFT JOIN departments ON employees.department_id = departments.id;
- **RIGHT JOIN (RIGHT OUTER JOIN)**: Returns all records from the right table and matched records from the left table.
  ```sh
  SELECT employees.name, departments.name 
  FROM employees 
  RIGHT JOIN departments ON employees.department_id = departments.id;
- **FULL JOIN (FULL OUTER JOIN)**: Returns all records when there is a match in either left or right table.
  ```sh
  SELECT employees.name, departments.name 
  FROM employees 
  FULL JOIN departments ON employees.department_id = departments.id;
- **CROSS JOIN**: Returns the Cartesian product of the two tables.
  ```sh
  SELECT employees.name, departments.name 
  FROM employees 
  CROSS JOIN departments;
- **SELF JOIN**: Joins a table to itself.
  ```sh
  SELECT e1.name, e2.name 
  FROM employees e1, employees e2 
  WHERE e1.manager_id = e2.id;

## Subqueries
- **Subqueries in SELECT**: Subquery within a SELECT statement.
  ```sh
   SELECT name, (SELECT department FROM departments WHERE departments.id = employees.department_id) AS department 
   FROM employees;
- **Subqueries in WHERE**: Subquery within a WHERE clause.
  ```sh
  SELECT * FROM employees 
  WHERE department_id = (SELECT id FROM departments WHERE name = 'HR');
- **Subqueries in FROM**: Subquery within a FROM clause.
  ```sh
  SELECT * FROM (SELECT * FROM employees WHERE age > 30) AS senior_employees;

## Set Operations
- **UNION**: Combines the result sets of two SELECT statements (removes duplicates).
  ```sh
  SELECT name FROM employees 
  UNION 
  SELECT name FROM contractors;
- **UNION ALL**: Combines the result sets of two SELECT statements (includes duplicates).
  ```sh
  SELECT name FROM employees 
  UNION ALL 
  SELECT name FROM contractors;
- **INTERSECT**: Returns common records from two SELECT statements.
  ```sh
  SELECT name FROM employees 
  INTERSECT 
  SELECT name FROM contractors;
- **EXCEPT**: Returns records from the first SELECT statement that are not in the second.
  ```sh
  SELECT name FROM employees 
  EXCEPT 
  SELECT name FROM contractors;

## Data Modification
- **INSERT**: Adds new rows to a table.
  ```sh
  INSERT INTO employees (name, age, department) VALUES ('Jane Doe', 28, 'Finance');
- **UPDATE**: Modifies existing rows in a table.
  ```sh
  UPDATE employees SET department = 'IT' WHERE name = 'Jane Doe';
- **DELETE**: Removes rows from a table.
  ```sh
  DELETE FROM employees WHERE name = 'Jane Doe';

## Indexing
- **CREATE INDEX**: Creates an index on a table.
  ```sh
  CREATE INDEX idx_name ON employees (name);
- **DROP INDEX**: Drops an index from a table.
  ```sh
  DROP INDEX idx_name ON employees;
- **UNIQUE INDEX**: Ensures all values in the index are unique.
  ```sh
  CREATE UNIQUE INDEX idx_unique_name ON employees (name);
- **FULL-TEXT INDEX**: Used for full-text searches.
  ```sh
  CREATE FULLTEXT INDEX idx_fulltext ON employees (name, department);
- **COMPOSITE INDEX**: Index on multiple columns.
  ```sh
  CREATE INDEX idx_composite ON employees (name, department);

## Transactions
- **BEGIN TRANSACTION**: Starts a transaction.
  ```sh
  BEGIN TRANSACTION;
- **COMMIT**: Commits the current transaction.
  ```sh
  COMMIT;
- **ROLLBACK**: Rolls back the current transaction.
  ```sh
  ROLLBACK;
- **SAVEPOINT**: Sets a savepoint within a transaction.
  ```sh
  SAVEPOINT savepoint1;
- **SET TRANSACTION ISOLATION LEVEL**: Sets the isolation level for the transaction.
  ```sh
  SET TRANSACTION ISOLATION LEVEL READ COMMITTED;

## Views
- **CREATE VIEW**: Creates a virtual table based on the result set of a SQL statement.
  ```sh
  CREATE VIEW hr_employees AS 
  SELECT * FROM employees WHERE department = 'HR';
- **DROP VIEW**: Deletes a view.
  ```sh
  DROP VIEW hr_employees;
- **ALTER VIEW**: Modifies a view.
  ```sh
  ALTER VIEW hr_employees AS 
  SELECT * FROM employees WHERE department = 'HR' AND age > 25;
- **INSERT INTO VIEW**: Inserts data into a view.
  ```sh
  INSERT INTO hr_employees (name, age, department) VALUES ('John Smith', 32, 'HR');
- **UPDATE VIEW**: Updates data in a view.
  ```sh
  UPDATE hr_employees SET age = 33 WHERE name = 'John Smith';
  
## Triggers
- **CREATE TRIGGER**: Creates a trigger that is executed when a specified event occurs.
  ```sh
  CREATE TRIGGER before_employee_insert 
  BEFORE INSERT ON employees 
  FOR EACH ROW 
  SET NEW.created_at = NOW();
- **DROP TRIGGER**: Deletes a trigger.
  ```sh
  DROP TRIGGER before_employee_insert;
- **AFTER INSERT/UPDATE/DELETE**: Trigger executed after the specified event.
  ```sh
  CREATE TRIGGER after_employee_insert 
  AFTER INSERT ON employees 
  FOR EACH ROW 
  INSERT INTO audit_log (action, employee_id) VALUES ('INSERT', NEW.id);
- **BEFORE INSERT/UPDATE/DELETE**: Trigger executed before the specified event.
  ```sh
  CREATE TRIGGER before_employee_update 
  BEFORE UPDATE ON employees 
  FOR EACH ROW 
  SET NEW.updated_at = NOW();

## Common Table Expressions (CTEs)
- **WITH CTE AS**: Defines a temporary result set that can be referenced within a SELECT, INSERT, UPDATE, or DELETE statement.
  ```sh
  WITH cte_employees AS (
    SELECT * FROM employees WHERE department = 'HR'
  )
  SELECT * FROM cte_employees;
- **RECURSIVE CTE**: A CTE that references itself.
  ```sh
  WITH RECURSIVE cte_numbers AS (
    SELECT 1 AS n
    UNION ALL
    SELECT n + 1 FROM cte_numbers WHERE n < 10
  )
  SELECT * FROM cte_numbers;
- **WITH TEMPORARY CTE**: A temporary CTE.
  ```sh
  WITH TEMPORARY cte_temp AS (
    SELECT * FROM employees WHERE age > 30
  )
  SELECT * FROM cte_temp;

## Window Functions
- **ROW_NUMBER()**: Assigns a unique number to each row.
  ```sh
  SELECT name, ROW_NUMBER() OVER (ORDER BY age) AS row_num FROM employees;
- **RANK()**: Assigns a rank to each row within a partition.
  ```sh
  SELECT name, RANK() OVER (ORDER BY age) AS rank FROM employees;
- **DENSE_RANK()**: Assigns a rank to each row within a partition without gaps.
  ```sh
  SELECT name, DENSE_RANK() OVER (ORDER BY age) AS dense_rank FROM employees;
- **NTILE()**: Distributes rows into a specified number of groups.
  ```sh
  SELECT name, NTILE(4) OVER (ORDER BY age) AS quartile FROM employees;
- **LEAD()**: Accesses data from a subsequent row.
  ```sh
  SELECT name, LEAD(name, 1) OVER (ORDER BY age) AS next_name FROM employees;
- **LAG()**: Accesses data from a previous row.
  ```sh
  SELECT name, LAG(name, 1) OVER (ORDER BY age) AS prev_name FROM employees;
- **FIRST_VALUE()**: Returns the first value in an ordered set of values.
  ```sh
  SELECT name, FIRST_VALUE(name) OVER (ORDER BY age) AS first_name FROM employees;
- **LAST_VALUE()**: Returns the last value in an ordered set of values.
  ```sh
  SELECT name, LAST_VALUE(name) OVER (ORDER BY age) AS last_name FROM employees;
- **SUM() OVER()**: Calculates a cumulative sum.
  ```sh
  SELECT name, age, SUM(age) OVER (ORDER BY age) AS cumulative_sum FROM employees;
- **AVG() OVER()**: Calculates a cumulative average.
  ```sh
  SELECT name, age, AVG(age) OVER (ORDER BY age) AS cumulative_avg FROM employees;
- **PARTITION BY**: Divides the result set into partitions.
  ```sh
  SELECT name, department, ROW_NUMBER() OVER (PARTITION BY department ORDER BY age) AS row_num FROM employees;
- **ORDER BY (WITHIN WINDOW FUNCTIONS)**: Orders rows within partitions.
  ```sh
  SELECT name, department, ROW_NUMBER() OVER (PARTITION BY department ORDER BY age DESC) AS row_num FROM employees;

## Date and Time Functions
- **GETDATE()**: Returns the current date and time.
  ```sh
  SELECT GETDATE() AS current_datetime;
- **CURRENT_TIMESTAMP**: Returns the current date and time.
  ```sh
  SELECT CURRENT_TIMESTAMP AS current_timestamp;
- **DATEADD()**: Adds a specified time interval to a date.
  ```sh
  SELECT DATEADD(year, 1, '2023-01-01') AS next_year;
- **DATEDIFF()**: Returns the difference between two dates.
  ```sh
  SELECT DATEDIFF(day, '2023-01-01', '2023-12-31') AS days_diff;
- **DATEPART()**: Returns a specified part of a date.
  ```sh
  SELECT DATEPART(year, '2023-01-01') AS year_part;
- **DATE_FORMAT()**: Formats a date.
  ```sh
  SELECT DATE_FORMAT('2023-01-01', '%Y-%m-%d') AS formatted_date;
- **NOW()**: Returns the current date and time.
  ```sh
  SELECT NOW() AS current_datetime;
- **EXTRACT()**: Extracts a part of a date.
  ```sh
  SELECT EXTRACT(year FROM '2023-01-01') AS year_extracted;
- **TIMESTAMPDIFF()**: Returns the difference between two timestamps.
  ```sh
  SELECT TIMESTAMPDIFF(day, '2023-01-01', '2023-12-31') AS days_diff;

## Conditional Logic
- **CASE WHEN**: Performs conditional logic in SQL.
  ```sh
  SELECT name, 
       CASE 
           WHEN age < 30 THEN 'Young' 
           WHEN age BETWEEN 30 AND 50 THEN 'Middle-aged' 
           ELSE 'Senior' 
       END AS age_group 
  FROM employees;
- **IFNULL()**: Returns a specified value if the expression is NULL.
  ```sh
    SELECT name, IFNULL(department, 'No Department') AS department FROM employees;
- **COALESCE()**: Returns the first non-null value in a list.
  ```sh
    SELECT name, COALESCE(department, 'No Department') AS department FROM employees;

---

- This comprehensive overview covers the essential aspects of SQL, including basic commands, filtering, sorting, aggregating data, joins, subqueries, set operations, data modification, indexing, transactions, views, triggers, CTEs, window functions, date and time functions, and conditional logic. Mastering these concepts will enable you to effectively manage and manipulate relational databases.
