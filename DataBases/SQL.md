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
By using the DISTINCT keyword in a **function called COUNT**, we can return the number of different countries.
```sql
SELECT COUNT(DISTINCT Country) FROM Customers;

SELECT Count(*) AS DistinctCountries
FROM (SELECT DISTINCT Country FROM Customers);
````

### 2. WHERE Clause
The WHERE clause is used to filter records.
```sql
# SQL requires single quotes around text values:
SELECT * FROM Customers WHERE Country='Mexico';

# However, numeric fields should not be enclosed in quotes:
SELECT * FROM Customers WHERE CustomerID=1;
````
### 3. ORDER BY
The ORDER BY keyword is used to sort the result-set in ascending or descending order.
```sql
SELECT * FROM Products ORDER BY Price;
SELECT * FROM Products ORDER BY Price DESC;
SELECT * FROM Customers ORDER BY Country, CustomerName;
SELECT * FROM Customers ORDER BY Country ASC, CustomerName DESC;
```

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
  
