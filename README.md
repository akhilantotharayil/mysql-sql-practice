---

# MySQL & NoSQL Basics

This repository contains SQL scripts and examples for learning **MySQL** database concepts including CRUD operations, table management, constraints, joins, transactions, functions, stored procedures, triggers, and more. It also briefly mentions **NoSQL** databases for comparison.

---

## Table of Contents

1. [Database Basics](#database-basics)
2. [NoSQL](#nosql)
3. [User Management](#user-management)
4. [Database & Table Operations](#database--table-operations)
5. [Data Types & Constraints](#data-types--constraints)
6. [CRUD Operations](#crud-operations)
7. [SQL Functions](#sql-functions)
8. [Transactions & Auto Commit](#transactions--auto-commit)
9. [Primary & Foreign Keys](#primary--foreign-keys)
10. [Joins](#joins)
11. [Views & Indexes](#views--indexes)
12. [Subqueries & Grouping](#subqueries--grouping)
13. [Stored Procedures](#stored-procedures)
14. [Triggers](#triggers)

---

## Database Basics

A **database** is an organized collection of data that can be easily accessed, managed, and updated. Databases are mainly of two types:

* **Relational (SQL)**: Data is stored in tables (MySQL, PostgreSQL).
* **Non-relational (NoSQL)**: Data is stored in flexible formats like JSON or key-value (MongoDB, Redis).

---

## NoSQL

NoSQL databases provide flexible schema design, high scalability, and are suited for large-scale or unstructured data.

---

## User Management

```sql
CREATE USER 'akhil'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'akhil'@'localhost' WITH GRANT OPTION;
```

* Creates a new database user and grants full privileges.

---

## Database & Table Operations

```sql
CREATE DATABASE akhil;
USE akhil;
CREATE TABLE users(...);
DROP DATABASE akhil;
```

* Create, use, and delete databases and tables.

---

## Data Types & Constraints

* **Data types**: INT, VARCHAR, DATE, TIMESTAMP, ENUM, BOOLEAN, DECIMAL.
* **Constraints**: PRIMARY KEY, UNIQUE, NOT NULL, AUTO_INCREMENT, FOREIGN KEY.

---

## CRUD Operations

* **Create / Insert**

```sql
INSERT INTO programmers VALUES (...);
```

* **Read / Select**

```sql
SELECT * FROM users WHERE gender = 'Male';
```

* **Update**

```sql
UPDATE programmers SET name = 'Akhil IPLit' WHERE id = 2;
```

* **Delete**

```sql
DELETE FROM programmers WHERE name = 'Pranavi';
```

---

## SQL Functions

* Aggregate: `COUNT()`, `MIN()`, `MAX()`, `AVG()`, `SUM()`
* String: `CONCAT()`, `LOWER()`, `UPPER()`, `LENGTH()`
* Math: `ROUND()`, `FLOOR()`, `CEIL()`, `MOD()`

---

## Transactions & Auto Commit

```sql
SET autocommit = 0;
COMMIT;
ROLLBACK;
SET autocommit = 1;
```

* Manage multiple operations as a single unit to ensure data integrity.

---

## Primary & Foreign Keys

* **Primary Key**: Unique identifier for table records.
* **Foreign Key**: Maintains referential integrity between tables.

```sql
CREATE TABLE addresses(
  id INT AUTO_INCREMENT PRIMARY KEY,
  user_id INT,
  CONSTRAINT fk_user FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

---

## Joins

* **INNER JOIN**: Returns matching rows from both tables.
* **LEFT JOIN / RIGHT JOIN**: Returns all rows from one table, matched rows from the other.
* **SELF JOIN**: Joins a table with itself.
* **UNION / UNION ALL**: Combine results from multiple queries.

---

## Views & Indexes

* **Views**: Virtual tables to simplify queries.

```sql
CREATE VIEW rich_users AS SELECT * FROM users WHERE salary > 70000;
```

* **Indexes**: Improve query performance.

```sql
CREATE INDEX idx_email ON users(gender);
```

---

## Subqueries & Grouping

* **Subqueries**: Query inside another query.
* **GROUP BY & HAVING**: Aggregate data based on columns.
* **ROLLUP**: Adds summary rows to grouped data.

---

## Stored Procedures

Encapsulate reusable SQL queries.

```sql
DELIMITER $$
CREATE PROCEDURE select_users()
BEGIN
  SELECT * FROM users;
END $$
DELIMITER ;
CALL select_users();
```

---

## Triggers

Automatically execute actions on table events.

```sql
CREATE TRIGGER after_user_insert
AFTER INSERT ON users
FOR EACH ROW
BEGIN
  INSERT INTO user_log(user_id,name) VALUES(NEW.id, NEW.name);
END;
```

---

This README provides a **quick reference** for MySQL beginners, with all essential commands, functions, and best practices in one place.

---



