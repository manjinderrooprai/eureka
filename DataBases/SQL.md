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

## Keywords in SQL

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

## **Types of SQL Operators**  

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


## **4.7Example Query Using Multiple Operators**
```sql
SELECT * FROM employees 
WHERE (salary > 50000 OR department = 'IT') 
AND age BETWEEN 25 AND 40 
AND name LIKE 'J%';
```

### **5. DML (Data Manipulation Language) Statements **  
DML (Data Manipulation Language) statements in SQL are used to **insert, update, delete, and retrieve** data from a database. These statements allow users to manipulate the data stored in database tables.  

## **5.1. `INSERT` Statement** (Adds new data to a table)  
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

## **5.2. `UPDATE` Statement** (Modifies existing data in a table)  
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

## **5.3. `DELETE` Statement** (Removes data from a table)  
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

## **5.4. `SELECT` Statement** (Retrieves data from a table)  
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
  
