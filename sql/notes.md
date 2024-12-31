## Aggregate Functions
- `COUNT` counts how many rows are in a particular column.
- `SUM` adds together all the values in a particular column.
- `MIN` and `MAX` return the lowest and highest values in a particular column, respectively.
- `AVG` calculates the average of a group of selected values.

```sql
SELECT COUNT(*)
  FROM tutorial.aapl_historical_stock_price

SELECT SUM(volume)
  FROM tutorial.aapl_historical_stock_price

SELECT MIN(volume) AS min_volume,
       MAX(volume) AS max_volume
  FROM tutorial.aapl_historical_stock_price

  SELECT AVG(high)
  FROM tutorial.aapl_historical_stock_price
```

### Order of Clauses
- SELECT
- FROM
- WHERE
- GROUP BY
- HAVING
- ORDER BY

## CRUD
- Create
- Read
- Update
- Delete

### Create Table

```sql
CREATE Table Users (
    Id INT PRIMARY KEY Identity(1,1),
    UserName NVARCHAR(50) NOT NULL,
    Email NVARCHAR(100) NOT Null,
    CreatedAt DATETIME DEFAULT GetDate()
)
```

```markdown 
#### Explanation
```

`id INT PRIMARY KEY IDENTITY(1,1)`
- id: This is the column name.
- INT: Specifies the data type as an integer.
- PRIMARY KEY: Indicates that id is the primary key, which uniquely identifies each record in the table.
- IDENTITY(1,1):
    - Configures the id column to auto-increment.
    - The first 1 specifies the seed (starting value of the auto-increment).
    - The second 1 specifies the increment (amount by which the val increases for each new row).

`username NVARCHAR(50) NOT NULL`
- NVARCHAR(50):
    - Defines the column as a Unicode string that can hold up to 50 characters.
    - The N in NVARCHAR ensures support for Unicode characters.
- NOT NULL:
    - Ensures that this column cannot contain NULL values; every record must have a value for username.

`created_at DATETIME DEFAULT GETDATE()`
- DATETIME:
    - Specifies the column type as a date and time value.
- DEFAULT GETDATE():
    - Automatically sets the current date and time when a new row is inserted.
- GETDATE() is a SQL Server function that retrieves the current system date and time.

### Insert Into
```sql
INSERT INTO Employees (EmployeeName, DepartmentID, HireDate)
    VALUES ('Tajinder Singh', '2', '2024-12-29');
```

### Update
```sql
UPDATE students
    SET name = "Tajinder Singh" WHERE id = 1;
```


## Cluases

#### `LIMIT`
to specify the number of records to return.

```sql
SELECT column_name(s) FROM table_name
    WHERE condition
    LIMIT 10; -- returns 10 records
```

#### `The MIN()`
function returns the smallest value of the selected column.
#### `The MAX()`
function returns the largest value of the selected column.
#### `The COUNT()`
function returns the number of rows that matches a specified criterion.
#### `The AVG()`
function returns the average value of a numeric column. 
#### `The SUM()`
function returns the total sum of a numeric column. 

### Wildcards

| Symbol | Description |
| -- | -- |
| %	| Represents zero or more characters |
| _ | Represents a single character      |

To understand
 - EXISTS

## Operators
### MySQL Arithmetic Operators
| Operator	| Description  |
| --------- | ------------ |
| +	| Add	 |
| -	| Subtract	 |
| *	| Multiply	 |
| /	| Divide	 |
| %	| Modulo	 |

### MySQL Bitwise Operators
| Operator	| Description |
| --------- | ----------- |
| &	 | Bitwise AND |
| \| | Bitwise OR |
| ^	 | Bitwise exclusive OR |

### MySQL Comparison Operators
| Operator	| Description |
| --------- | ----------- |
| =	| Equal to	 |
| >	| Greater than	 |
| <	| Less than	 |
| >=	| Greater than or equal to	 |
| <=	| Less than or equal to	 |
| <>	| Not equal to |

## Constraints
- constraints are used to specify rules for data in a table.
- Constraints can be specified when the table is created with the 
    - CREATE TABLE statement, or 
    - after the table is created with the ALTER TABLE statement.

Types of constraints
- NOT NULL - Ensures that a column cannot have a NULL value
- UNIQUE - Ensures that all values in a column are different
- PRIMARY KEY - A combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table
- FOREIGN KEY - Prevents actions that would destroy links between tables
- CHECK - Ensures that the values in a column satisfies a specific condition
- DEFAULT - Sets a default value for a column if no value is specified
- CREATE INDEX - Used to create and retrieve data from the database very quickly

### Primary & Foreign Key
```sql
CREATE TABLE Orders (
    OrderID int PRIMARY KEY,
    OrderNumber int NOT NULL,
    PersonID int,
    CONSTRAINT FK_PersonOrder FOREIGN KEY (PersonID)
    REFERENCES Persons(PersonID)
);

ALTER TABLE Orders
ADD CONSTRAINT FK_PersonOrder
FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);

ALTER TABLE Orders
DROP FOREIGN KEY FK_PersonOrder;

```

### Check
```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    City varchar(255),
    CONSTRAINT CHK_Person CHECK (Age>=18)
);

ALTER TABLE Persons
ADD CONSTRAINT CHK_Person CHECK (Age>=18)

ALTER TABLE Persons
DROP CHECK CHK_Person;

```

### Default
```sql
CREATE Table Users (
    Id INT PRIMARY KEY Identity(1,1),
    UserName NVARCHAR(50) NOT NULL,
    Email NVARCHAR(100) NOT Null,
    CreatedAt DATETIME DEFAULT GetDate()
)

ALTER TABLE Users
ALTER CreatedAt SET DEFAULT GetDate();

ALTER TABLE Users
ALTER CreatedAt DROP DEFAULT;
```

### Identity (auto increment)
```sql
CREATE Table Users (
    Id INT PRIMARY KEY Identity(1,1),
    UserName NVARCHAR(50) NOT NULL,
    Email NVARCHAR(100) NOT Null,
    CreatedAt DATETIME DEFAULT GetDate()
)
```

## Views
### Create Views

```sql
CREATE VIEW [Brazil Customers] AS
SELECT CustomerName, ContactName
FROM Customers
WHERE Country = 'Brazil';

CREATE VIEW [Products Above AVG Price]
SELECT ProductName, Price
FROM Products
WHERE Price > (SELECT AVG(Price) FROM Products);
```

### Update Views
```sql
CREATE OR REPLACE VIEW [Brazil Customers] AS
SELECT CustomerName, ContactName, City
FROM Customers
WHERE Country = 'Brazil';
```

### Drop Views
```sql
DROP VIEW [Brazil Customers];
```

## Procedures in SQL

- A **stored procedure** in SQL is a precompiled set of SQL statements that can be stored in a database and reused. 
- It encapsulates logic and can accept input and output parameters, making it useful for automating tasks, reusing logic, and improving performance.

### Create Stored Procedure

```sql
CREATE PROCEDURE GetEmployeeCountByDepartment
    @DepartmentID INT,
    @HiringDate DATE,
    @EmployeeCount INT OUTPUT
AS
BEGIN 
    SELECT @EmployeeCount = COUNT(*)
    FROM Employees
    WHERE DepartmentID = @DepartmentID;
    AND HireDate = @HiringDate
END

-- With try - catch

CREATE PROCEDURE GetEmployeeCountByDepartment
    @DepartmentID INT,
    @HiringDate DATE,
    @EmployeeCount INT OUTPUT
AS
BEGIN 
    BEGIN TRY
        SELECT @EmployeeCount = COUNT(*)
        FROM Employees
        WHERE DepartmentID = @DepartmentID;
        AND HireDate = @HiringDate
    END TRY
    BEGIN CATCH
        SELECT ERROR_MESSAGE() AS ErrorMessage;
    END CATCH;
END;
```

### Execute Store Procedure

```sql
DECLARE @Count INT;
EXEC GetEmployeeCountByDepartment @DepartmentID = 3, @HiringDate = '2021-11-15', @EmployeeCount = @Count OUTPUT;
PRINT @Count;
```

### Altering procedure
```sql
ALTER PROCEDURE GetAllEmployees
AS
BEGIN
    SELECT EmployeeID, EmployeeName FROM Employees;
END;
```

### Drop procedure
```sql
DROP PROCEDURE GetAllEmployees;
```

## Functions
### Create Function

```sql
CREATE FUNCTION TotalSalaryByDepartment (@DepartmentID INT)
RETURNS FLOAT
AS
BEGIN
    DECLARE @TotalSalary FLOAT;
    SELECT @TotalSalary = SUM(Salary)
    FROM Employees
    WHERE DepartmentID = @DepartmentID;
    RETURN @TotalSalary;
END;
```

### Invoke Function
```sql
SELECT dbo.TotalSalaryByDepartment(2) AS TotalSalary;
```

## **SQL Data Types**

In SQL, data types define the kind of values a column can hold. They vary slightly between different database systems like MySQL, SQL Server, Oracle, and PostgreSQL. Below is a general overview of commonly used SQL data types.

### **1. String Data Types**
| Data Type         | Description                                                                 | Example                     |
|--------------------|-----------------------------------------------------------------------------|-----------------------------|
| `CHAR(size)`       | Fixed-length string. Max size: 255 characters.                             | `CHAR(10)` stores "Hello   " |
| `VARCHAR(size)`    | Variable-length string. Max size: 65535 characters.                        | `VARCHAR(50)` stores "Hello" |
| `TEXT`             | Large text data. Max size varies by DB (e.g., 2GB in SQL Server).          | Stores paragraphs of text   |
| `NCHAR(size)`      | Fixed-length Unicode string.                                               | `NCHAR(10)`                 |
| `NVARCHAR(size)`   | Variable-length Unicode string.                                            | `NVARCHAR(50)`              |
| `NTEXT`            | Deprecated in SQL Server. Use `NVARCHAR(MAX)` instead.                     |                              |

---

### **2. Numeric Data Types**
| Data Type         | Description                                                                 | Example                     |
|--------------------|-----------------------------------------------------------------------------|-----------------------------|
| `TINYINT`          | Integer between 0 and 255 (unsigned) or -128 to 127 (signed).              | `TINYINT` (value: 100)      |
| `SMALLINT`         | Integer between -32,768 and 32,767.                                        | `SMALLINT` (value: 3000)    |
| `INT` / `INTEGER`  | Integer between -2,147,483,648 and 2,147,483,647.                          | `INT` (value: 123456)       |
| `BIGINT`           | Integer between -9,223,372,036,854,775,808 and 9,223,372,036,854,775,807. | `BIGINT` (value: 123456789) |
| `DECIMAL(p, s)`    | Fixed-point number. `p` is precision, `s` is scale.                       | `DECIMAL(10,2)` stores `12345.67` |
| `NUMERIC(p, s)`    | Synonym for `DECIMAL`.                                                     |                              |
| `FLOAT(p)`         | Approximate floating-point number. Precision depends on `p`.              | `FLOAT(24)` (value: 1.2345) |
| `REAL`             | Floating-point number with less precision than `FLOAT`.                   |                              |

---

### **3. Date and Time Data Types**
| Data Type         | Description                                                                 | Example                     |
|--------------------|-----------------------------------------------------------------------------|-----------------------------|
| `DATE`             | Stores date in `YYYY-MM-DD` format.                                        | `2024-12-29`                |
| `DATETIME`         | Stores date and time in `YYYY-MM-DD HH:MM:SS` format.                      | `2024-12-29 13:45:30`       |
| `TIMESTAMP`        | Stores date and time with automatic time-zone adjustment.                  | `2024-12-29 13:45:30`       |
| `TIME`             | Stores time in `HH:MM:SS` format.                                          | `13:45:30`                  |
| `YEAR`             | Stores year in 2 or 4 digits.                                              | `2024`                      |

---

### **4. Boolean Data Type**
| Data Type         | Description                                                                 | Example                     |
|--------------------|-----------------------------------------------------------------------------|-----------------------------|
| `BOOLEAN`          | Stores TRUE or FALSE. Often implemented as `TINYINT(1)` internally.        | `TRUE`, `FALSE`, `0`, `1`   |

---

### **5. Binary Data Types**
| Data Type         | Description                                                                 | Example                     |
|--------------------|-----------------------------------------------------------------------------|-----------------------------|
| `BINARY(size)`     | Fixed-length binary data.                                                   |                              |
| `VARBINARY(size)`  | Variable-length binary data.                                                |                              |
| `BLOB`             | Binary large object for storing binary data like images or files.          |                              |

---

### **6. Spatial Data Types** (Optional: Based on DB support)
| Data Type         | Description                                                                 | Example                     |
|--------------------|-----------------------------------------------------------------------------|-----------------------------|
| `GEOMETRY`         | Stores geometric data.                                                     |                              |
| `POINT`            | Stores a single point.                                                     |                              |
| `LINESTRING`       | Stores a line.                                                             |                              |
| `POLYGON`          | Stores a polygon.                                                         |                              |

---

### **7. JSON and XML Data Types**
| Data Type         | Description                                                                 | Example                     |
|--------------------|-----------------------------------------------------------------------------|-----------------------------|
| `JSON`             | Stores JSON-formatted data. Supported in MySQL, PostgreSQL, etc.           | `{ "name": "John" }`        |
| `XML`              | Stores XML data. Supported in SQL Server, Oracle, etc.                     | `<name>John</name>`         |


## Differences
### Where vs Having

| Feature            | `WHERE` Clause                        | `HAVING` Clause                      |
|---------------------|---------------------------------------|---------------------------------------|
| **Purpose**         | Filters rows before grouping.         | Filters groups after grouping.        |
| **Execution Stage** | Executes before `GROUP BY`.           | Executes after `GROUP BY`.            |
| **Applies To**      | Individual rows.                     | Aggregated data (e.g., groups).       |
| **Aggregate Functions** | Cannot use aggregate functions.     | Can use aggregate functions.          |
| **Usage**           | General filtering of rows.           | Filtering grouped or aggregated data. |

### Procedures and Functions
| Aspect                   | Procedure                                   | Function                                    |
|--------------------------|---------------------------------------------|--------------------------------------------|
| **Purpose**              | Used to perform a set of operations, such as data manipulation or administrative tasks. | Designed to compute and return a value based on inputs. |
| **Return Value**         | May return multiple values via output parameters or no value at all. | Always returns a single value of a specific data type. |
| **Usage in Queries**     | Cannot be called directly in a SQL query.  | Can be called directly in a SQL query.     |
| **Output**               | Can perform actions like `INSERT`, `UPDATE`, and `DELETE`. | Primarily used for computations and returns data without modifying the database. |
| **Parameters**           | Supports `IN`, `OUT`, and `INOUT` parameters. | Only supports `IN` parameters.             |
| **Transaction Control**  | Allows the use of transaction statements like `COMMIT` and `ROLLBACK`. | Cannot include transaction control statements. |
| **Calling Syntax**       | Invoked using `EXEC` or `EXECUTE`.          | Called as part of a SQL expression (e.g., `SELECT`). |
| **Dependency**           | Typically operates independently of queries. | Typically used within SQL queries or procedures. |
| **Error Handling**       | Can include error handling with `TRY...CATCH`. | Limited error handling; exceptions are propagated. |


### When to use 
| **Use Case**                           | **Choose Procedure** | **Choose Function** |
|----------------------------------------|-----------------------|----------------------|
| Perform actions like `INSERT`, `UPDATE`, or `DELETE`. | &#x2714;                    | ❌                   |
| Return a computed value to a query.    | ❌                    | &#x2714;                   |
| Complex logic with multiple outputs.   | &#x2714;                    | ❌                   |
| Use in views or other SQL queries.     | ❌                    | &#x2714;                   |
| Need transaction control.              | &#x2714;                    | ❌                   | 