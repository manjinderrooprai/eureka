# SQL
SQL stands for Structured Query Language and It lets you access and manipulate databases. SQL became a standard of the American National Standards Institute (ANSI) in 1986, and of the International Organization for Standardization (ISO) in 1987.

## **Key Features of SQL**
1. **Declarative Language** – You describe *what* data you need, not *how* to retrieve it.  
2. **Standardized Language** – It follows **ANSI and ISO standards**, making it widely used.  
3. **Highly Scalable** – Works with both small applications and large enterprise databases.  
4. **Supports Multiple Operations** – CRUD (Create, Read, Update, Delete) operations for database management.  
5. **Security Features** – User authentication, access control, and encryption capabilities.  

## **Uses of SQL**
SQL is used in various domains such as **web applications, banking, e-commerce, data analytics, and enterprise software**.  

## **Types of SQL Commands**
SQL commands are categorized into five main types:  

| Type | Description | Example |
|------|------------|---------|
| **DDL (Data Definition Language)** | Defines database structure | `CREATE`, `ALTER`, `DROP` |
| **DML (Data Manipulation Language)** | Modifies database records | `INSERT`, `UPDATE`, `DELETE` |
| **DQL (Data Query Language)** | Retrieves data | `SELECT` |
| **DCL (Data Control Language)** | Controls database access | `GRANT`, `REVOKE` |
| **TCL (Transaction Control Language)** | Manages transactions | `COMMIT`, `ROLLBACK` |

### **1. Data Retrieval**
SQL helps retrieve specific data from a database using queries.  
Example:  
```sql
SELECT name, age FROM employees WHERE department = 'IT';
```

### **2. Data Manipulation**
SQL allows adding, updating, and deleting records in a database.  
Example:  
```sql
INSERT INTO employees (name, age, department) VALUES ('John Doe', 30, 'HR');
```
```sql
UPDATE employees SET age = 31 WHERE name = 'John Doe';
```
```sql
DELETE FROM employees WHERE name = 'John Doe';
```

### **3. Database Management**
SQL provides commands for database administration, such as creating and modifying tables.  
Example:  
```sql
CREATE DATABASE CompanyDB;
CREATE TABLE employees (id INT PRIMARY KEY, name VARCHAR(50), age INT);
```

### **4. Data Filtering and Aggregation**
SQL helps analyze and summarize data using functions like `COUNT()`, `SUM()`, `AVG()`, etc.  
Example:  
```sql
SELECT department, COUNT(*) FROM employees GROUP BY department HAVING COUNT(*) > 5;
```

### **5. Joining Tables**
SQL allows combining data from multiple tables using `JOIN`.  
Example:  
```sql
SELECT employees.name, departments.department_name 
FROM employees
JOIN departments ON employees.department_id = departments.id;
```

### **6. Security and Access Control**
SQL manages database security through access control commands.  
Example:  
```sql
GRANT SELECT, INSERT ON employees TO 'user123'@'localhost';
```

### **7. Transactions & ACID Compliance**
SQL supports transactions to ensure **data consistency and reliability**.  
Example:  
```sql
BEGIN TRANSACTION;
UPDATE accounts SET balance = balance - 500 WHERE id = 1;
UPDATE accounts SET balance = balance + 500 WHERE id = 2;
COMMIT;
```

## Keywords

### 1. DISTINCT
It used to remove duplicate values from a query result and return only unique records.
```sql
SELECT DISTINCT Country FROM Customers;
````

### 1.1 COUNT(DISTINCT)
By using the **DISTINCT** keyword in a **function called COUNT**, we can return the number of different countries.
```sql
SELECT COUNT(DISTINCT Country) FROM Customers;

SELECT Count(*) AS DistinctCountries
FROM (SELECT DISTINCT Country FROM Customers);
````

### 2. WHERE
The **WHERE** clause is used to filter records.
```sql
# SQL requires single quotes around text values:
SELECT * FROM Customers WHERE Country='Mexico';

# However, numeric fields should not be enclosed in quotes:
SELECT * FROM Customers WHERE CustomerID=1;
````
### 3. ORDER BY
The **ORDER BY** keyword is used to sort the result-set in ascending or descending order.
```sql
SELECT * FROM Products ORDER BY Price;
SELECT * FROM Products ORDER BY Price DESC;
SELECT * FROM Customers ORDER BY Country, CustomerName;
SELECT * FROM Customers ORDER BY Country ASC, CustomerName DESC;
```

### 4. Operators:
Operators in SQL are **symbols or keywords** used to perform operations on data. They are mainly used in **WHERE, SELECT, and HAVING** clauses to filter, compare, and manipulate data.
### **Types of SQL Operators**  

### **4.1. Arithmetic Operators** *(Used for mathematical calculations)*
| Operator | Description | Example |
|----------|------------|---------|
| `+`  | Addition | `SELECT 10 + 5;` → **15** |
| `-`  | Subtraction | `SELECT 10 - 5;` → **5** |
| `*`  | Multiplication | `SELECT 10 * 5;` → **50** |
| `/`  | Division | `SELECT 10 / 5;` → **2** |
| `%`  | Modulus (Remainder) | `SELECT 10 % 3;` → **1** |

### **4.2. Comparison (Relational) Operators** *(Used for filtering data)*
| Operator | Description | Example |
|----------|------------|---------|
| `=`  | Equal to | `SELECT * FROM employees WHERE age = 30;` |
| `!=` or `<>` | Not equal to | `SELECT * FROM employees WHERE age <> 30;` |
| `>`  | Greater than | `SELECT * FROM employees WHERE salary > 50000;` |
| `<`  | Less than | `SELECT * FROM employees WHERE age < 25;` |
| `>=` | Greater than or equal to | `SELECT * FROM employees WHERE age >= 40;` |
| `<=` | Less than or equal to | `SELECT * FROM employees WHERE age <= 50;` |

### **4.3. Logical Operators** *(Used to combine multiple conditions)*
| Operator | Description | Example |
|----------|------------|---------|
| `AND`  | Returns true if **both** conditions are true | `SELECT * FROM employees WHERE age > 25 AND salary > 50000;` |
| `OR`  | Returns true if **at least one** condition is true | `SELECT * FROM employees WHERE age < 25 OR department = 'HR';` |
| `NOT`  | Reverses the condition | `SELECT * FROM employees WHERE NOT department = 'IT';` |

### **4.4. Bitwise Operators** *(Used for bitwise operations on numbers)*
| Operator | Description | Example |
|----------|------------|---------|
| `&`  | Bitwise AND | `SELECT 5 & 3;` → **1** |
| `|`  | Bitwise OR | `SELECT 5 | 3;` → **7** |
| `^`  | Bitwise XOR | `SELECT 5 ^ 3;` → **6** |
| `~`  | Bitwise NOT | `SELECT ~5;` (Result depends on system) |

### **4.5. String Operators** *(Used to compare or manipulate strings)*
| Operator | Description | Example |
|----------|------------|---------|
| `LIKE`  | Matches a pattern | `SELECT * FROM employees WHERE name LIKE 'A%';` (Names starting with 'A') |
| `ILIKE` | Case-insensitive pattern match (PostgreSQL) | `SELECT * FROM employees WHERE name ILIKE 'john%';` |
| `||` | String concatenation (Some databases use `+`) | `SELECT 'Hello' || ' World';` → **Hello World** |

### **4.6. Special Operators** *(Used for advanced filtering)*
| Operator | Description | Example |
|----------|------------|---------|
| `IN` | Matches any value in a list | `SELECT * FROM employees WHERE department IN ('IT', 'HR', 'Sales');` |
| `NOT IN` | Excludes values in a list | `SELECT * FROM employees WHERE department NOT IN ('HR', 'Sales');` |
| `BETWEEN` | Checks if value is in a range | `SELECT * FROM employees WHERE salary BETWEEN 30000 AND 60000;` |
| `IS NULL` | Checks if value is NULL | `SELECT * FROM employees WHERE age IS NULL;` |
| `IS NOT NULL` | Checks if value is NOT NULL | `SELECT * FROM employees WHERE age IS NOT NULL;` |
| `EXISTS` | Checks if a subquery returns results | `SELECT * FROM employees WHERE EXISTS (SELECT 1 FROM departments WHERE department = 'IT');` |

### **4.7 Example Query Using Multiple Operators**
```sql
SELECT * FROM employees 
WHERE (salary > 50000 OR department = 'IT') 
AND age BETWEEN 25 AND 40 
AND name LIKE 'J%';
```

### **5. DML (Data Manipulation Language) Statements**  
DML (Data Manipulation Language) statements in SQL are used to **insert, update, delete, and retrieve** data from a database. These statements allow users to manipulate the data stored in database tables.  

### **5.1. `INSERT` Statement** (Adds new data to a table)  
Used to insert new rows into a table.  

### **Syntax:**
```sql
INSERT INTO table_name (column1, column2, column3)  
VALUES (value1, value2, value3);
```

### **Example:**
```sql
INSERT INTO employees (id, name, department, salary)  
VALUES (1, 'John Doe', 'IT', 60000);
```
✅ Adds a new employee to the `employees` table.

### **5.2. `UPDATE` Statement** (Modifies existing data in a table)  
Used to update existing records in a table.

### **Syntax:**
```sql
UPDATE table_name  
SET column1 = value1, column2 = value2  
WHERE condition;
```

### **Example:**
```sql
UPDATE employees  
SET salary = 70000  
WHERE name = 'John Doe';
```
✅ Updates the salary of **John Doe** in the `employees` table.

⚠️ **Without a `WHERE` clause, all rows will be updated!**

### **5.3. `DELETE` Statement** (Removes data from a table)  
Used to delete specific rows from a table.

### **Syntax:**
```sql
DELETE FROM table_name  
WHERE condition;
```

### **Example:**
```sql
DELETE FROM employees  
WHERE department = 'HR';
```
✅ Deletes all employees in the **HR** department.

⚠️ **Without a `WHERE` clause, all rows will be deleted!**

### **5.4. `SELECT` Statement** (Retrieves data from a table)  
Used to fetch data from a database.

### **Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```

### **Example:**
```sql
SELECT name, salary  
FROM employees  
WHERE department = 'IT';
```
✅ Retrieves the **name and salary** of all employees in the **IT** department.

### 6. Clauses:
Clauses are used to **limit the number of rows** returned by a SQL query. Different databases use different keywords for this functionality.

### **Comparison Table**
| Clause | Database | Usage Example |
|--------|----------|--------------|
| `TOP` | SQL Server | `SELECT TOP 5 * FROM employees;` |
| `LIMIT` | MySQL, PostgreSQL | `SELECT * FROM employees LIMIT 5;` |
| `FETCH FIRST` | Oracle 12c+, PostgreSQL | `SELECT * FROM employees FETCH FIRST 5 ROWS ONLY;` |
| `ROWNUM` | Oracle | `SELECT * FROM employees WHERE ROWNUM <= 5;` |

### **Conclusion**
- Use `TOP` in **SQL Server**.
- Use `LIMIT` in **MySQL and PostgreSQL**.
- Use `FETCH FIRST` in **Oracle 12c+ and PostgreSQL**.
- Use `ROWNUM` in **older Oracle versions**.

### **7. Aggregate Functions**  
SQL **aggregate functions** perform calculations on a set of values and return a **single** result. These functions are commonly used with the `GROUP BY` clause.  

### **7.1. COUNT()**  
👉 **Counts the number of rows** in a result set.  

📌 **Example:**  
```sql
SELECT COUNT(*) AS total_employees FROM employees;
```
✅ **Returns** the total number of employees.


### **7.2. SUM()**  
👉 **Calculates the total sum** of a numeric column.  

📌 **Example:**  
```sql
SELECT SUM(salary) AS total_salary FROM employees;
```
✅ **Returns** the sum of all employee salaries.


### **7.3. AVG()**  
👉 **Finds the average value** of a numeric column.  

📌 **Example:**  
```sql
SELECT AVG(salary) AS average_salary FROM employees;
```
✅ **Returns** the average salary of employees.


### **7.4. MIN()**  
👉 **Finds the minimum value** in a column.  

📌 **Example:**  
```sql
SELECT MIN(salary) AS lowest_salary FROM employees;
```
✅ **Returns** the lowest salary in the table.


### **7.5. MAX()**  
👉 **Finds the maximum value** in a column.  

📌 **Example:**  
```sql
SELECT MAX(salary) AS highest_salary FROM employees;
```
✅ **Returns** the highest salary in the table.


### **7.6. GROUP BY with Aggregate Functions**  
👉 **Used to group results** before applying an aggregate function.  

📌 **Example:** Get the total salary for each department:  
```sql
SELECT department, SUM(salary) AS total_salary  
FROM employees  
GROUP BY department;
```
✅ **Returns** the total salary for each department.


### **7.7. HAVING with Aggregate Functions**  
👉 **Filters grouped records** based on aggregate function conditions.  

📌 **Example:** Show departments where the total salary is more than 500,000:  
```sql
SELECT department, SUM(salary) AS total_salary  
FROM employees  
GROUP BY department  
HAVING SUM(salary) > 500000;
```
✅ **Filters** groups based on aggregate conditions.

### **Summary Table**
| Function | Description | Example |
|----------|-------------|---------|
| `COUNT()` | Counts rows | `COUNT(*)` |
| `SUM()` | Adds values | `SUM(salary)` |
| `AVG()` | Calculates average | `AVG(salary)` |
| `MIN()` | Finds minimum | `MIN(salary)` |
| `MAX()` | Finds maximum | `MAX(salary)` |

### **8. Joins**  
👉 **Joins** in SQL are used to **combine rows** from two or more tables based on a **related column**.  

### **Types of Joins**
### **8.1. INNER JOIN** (Most Common)  
✅ Returns only **matching rows** from both tables.  

📌 **Example:** Get employees and their department names  
```sql
SELECT employees.name, departments.department_name  
FROM employees  
INNER JOIN departments ON employees.department_id = departments.id;
```
✅ **Only employees with a matching department appear** in the result.


### **8.2. LEFT JOIN (LEFT OUTER JOIN)**  
✅ Returns **all rows from the left table** and **matching rows from the right table** (if no match, NULL is returned).  

📌 **Example:** Get all employees, including those without a department  
```sql
SELECT employees.name, departments.department_name  
FROM employees  
LEFT JOIN departments ON employees.department_id = departments.id;
```
✅ Employees without a department will have `NULL` in `department_name`.

### **8.3. RIGHT JOIN (RIGHT OUTER JOIN)**  
✅ Returns **all rows from the right table** and **matching rows from the left table** (if no match, NULL is returned).  

📌 **Example:** Get all departments, even those with no employees  
```sql
SELECT employees.name, departments.department_name  
FROM employees  
RIGHT JOIN departments ON employees.department_id = departments.id;
```
✅ Departments without employees will have `NULL` in `employees.name`.

### **8.4. FULL JOIN (FULL OUTER JOIN)**  
✅ Returns **all rows from both tables**, filling `NULL` where there’s no match.  

📌 **Example:** Get all employees and all departments, even if they don’t match  
```sql
SELECT employees.name, departments.department_name  
FROM employees  
FULL JOIN departments ON employees.department_id = departments.id;
```
✅ Unmatched employees and departments will show `NULL` in missing columns.

### **8.5. CROSS JOIN**  
✅ **Cartesian product** – returns all possible combinations of rows from both tables.  

📌 **Example:** Get all combinations of employees and departments  
```sql
SELECT employees.name, departments.department_name  
FROM employees  
CROSS JOIN departments;
```
✅ If there are 10 employees and 5 departments, **50 rows** will be returned.

### **8.6. SELF JOIN**  
✅ Joins a table **to itself**, useful for **hierarchical relationships** (e.g., managers & employees).  

📌 **Example:** Get employees and their managers  
```sql
SELECT e1.name AS Employee, e2.name AS Manager  
FROM employees e1  
LEFT JOIN employees e2 ON e1.manager_id = e2.id;
```
✅ Returns employee names and their managers.

### **Comparison Table**
| Join Type | Includes Matching Rows | Includes Non-Matching Rows |
|-----------|----------------------|---------------------------|
| **INNER JOIN** | ✅ Yes | ❌ No |
| **LEFT JOIN** | ✅ Yes | ✅ From Left Table |
| **RIGHT JOIN** | ✅ Yes | ✅ From Right Table |
| **FULL JOIN** | ✅ Yes | ✅ From Both Tables |
| **CROSS JOIN** | ✅ Yes (All Combinations) | ❌ No |
| **SELF JOIN** | ✅ Yes | ✅ (Self-Join Use Case) |

## **SQL Stored Procedure**  
👉 A **Stored Procedure** is a **precompiled set of SQL statements** stored in the database that can be **executed multiple times** with different parameters.  

### **Why Use Stored Procedures?**  
✅ **Reusability** – Write once, use multiple times.  
✅ **Performance** – Precompiled, runs faster than executing raw queries.  
✅ **Security** – Prevents SQL injection by using parameters.  
✅ **Reduces Network Traffic** – Executes on the database server, minimizing data transfer.  

### **Syntax: Creating a Stored Procedure**  
📌 **Example:** Create a stored procedure to fetch employees by department  
```sql
DELIMITER $$  
CREATE PROCEDURE GetEmployeesByDept(IN dept_id INT)  
BEGIN  
    SELECT * FROM employees WHERE department_id = dept_id;  
END $$  
DELIMITER ;
```
✅ **`IN dept_id INT`** – Takes department ID as input.  
✅ **`SELECT * FROM employees`** – Fetches employees from that department.  

### **Executing a Stored Procedure**  
📌 **Example:** Call the procedure for department `5`  
```sql
CALL GetEmployeesByDept(5);
```
✅ Retrieves all employees from department **5**.

### **Stored Procedure with Multiple Parameters**  
📌 **Example:** Insert a new employee  
```sql
DELIMITER $$  
CREATE PROCEDURE AddEmployee(IN emp_name VARCHAR(50), IN dept_id INT, IN salary DECIMAL(10,2))  
BEGIN  
    INSERT INTO employees (name, department_id, salary)  
    VALUES (emp_name, dept_id, salary);  
END $$  
DELIMITER ;
```
✅ Adds a new employee with **name, department ID, and salary**.

📌 **Calling the Procedure**  
```sql
CALL AddEmployee('John Doe', 3, 75000.00);
```
✅ Inserts **John Doe** into department **3** with a salary of **75,000**.

### **Stored Procedure with Output Parameter**  
📌 **Example:** Get employee count from a department  
```sql
DELIMITER $$  
CREATE PROCEDURE GetEmployeeCount(IN dept_id INT, OUT emp_count INT)  
BEGIN  
    SELECT COUNT(*) INTO emp_count FROM employees WHERE department_id = dept_id;  
END $$  
DELIMITER ;
```
✅ `OUT emp_count INT` – Stores the result in `emp_count`.  

📌 **Executing the Procedure**  
```sql
CALL GetEmployeeCount(3, @total);  
SELECT @total AS EmployeeCount;
```
✅ Retrieves **total employees in department 3**.


### **Modifying & Deleting a Stored Procedure**  
📌 **Modify a Stored Procedure**  
```sql
DROP PROCEDURE IF EXISTS GetEmployeesByDept;  
```
📌 **Delete a Stored Procedure**  
```sql
ALTER PROCEDURE GetEmployeesByDept …;  -- Not supported in all databases
```
✅ **To modify, drop and recreate the procedure**.

### **Conclusion**
Stored procedures **enhance performance, security, and maintainability** in SQL. Need help with **advanced procedures like loops or transactions?** 🚀

## **Popular SQL Database Management Systems**
SQL is used in various RDBMS (Relational Database Management Systems), including:
1. **MySQL** – Open-source, widely used in web applications.  
2. **PostgreSQL** – Advanced open-source database with high security.  
3. **SQL Server** – Developed by Microsoft, used in enterprise applications.  
4. **Oracle Database** – High-performance database used in large organizations.  
5. **SQLite** – Lightweight, embedded database used in mobile apps.  

## **SQL vs. NoSQL**
| Feature | SQL (Relational) | NoSQL (Non-Relational) |
|---------|----------------|----------------|
| **Structure** | Tables with rows & columns | Collections, key-value pairs, graphs |
| **Schema** | Fixed schema | Flexible schema |
| **Scalability** | Vertical scaling | Horizontal scaling |
| **Examples** | MySQL, PostgreSQL, SQL Server | MongoDB, Cassandra, Redis |

## **Conclusion**
SQL is the **backbone of modern data management**, helping organizations efficiently store, retrieve, and manipulate data. Whether it's **web applications, financial systems, or data analytics**, SQL remains a crucial tool for handling structured data.
  
