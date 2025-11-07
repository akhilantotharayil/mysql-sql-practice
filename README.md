---

# 🗄️ MySQL Notes

A complete guide to understanding and practicing **MySQL** — from user creation and database setup to joins, transactions, and triggers.

---

## 📚 Table of Contents

1. [What is a Database?](#-what-is-a-database)
2. [What is NoSQL?](#-what-is-nosql)
3. [Creating a User and Granting Privileges](#-creating-a-user-and-granting-privileges)
4. [Creating and Using a Database](#-creating-and-using-a-database)
5. [Creating a Table](#-creating-a-table)
6. [Selecting Data](#-selecting-data)
7. [Dropping a Database](#-dropping-a-database)
8. [Logging into the Database](#-logging-into-the-database)
9. [Running SQL Scripts in Docker](#-running-sql-scripts-in-docker)
10. [sqlscript.sql Example](#-sqlscriptsql-example)
11. [Datatypes and Constraints](#-datatypes-and-constraints)
12. [Renaming a Table](#-renaming-a-table)
13. [Altering a Table](#-altering-a-table)
14. [Inserting Data](#-inserting-data)
15. [Querying Data](#-querying-data)
16. [Updating Data](#-updating-data)
17. [Deleting Data](#-deleting-data)
18. [Dropping a Table](#-dropping-a-table)
19. [Constraints in Detail](#-constraints-in-detail)
20. [MySQL Functions](#-mysql-functions)
21. [Mathematical Functions](#-mathematical-functions)
22. [Adding Columns and UUIDs](#-adding-columns-and-uuids)
23. [MOD, LOWER, UPPER, CONCAT](#-mod-lower-upper-concat)
24. [Copying Table Structure and Data](#-copying-table-structure-and-data)
25. [Transactions](#-transactions)
26. [Primary Key and Auto Increment](#-primary-key-and-auto-increment)
27. [Foreign Keys](#-foreign-keys)
28. [MySQL Joins](#-mysql-joins)
29. [UNION and UNION ALL](#-union-and-union-all)
30. [SELF JOIN](#-self-join)
31. [Views](#-views)
32. [Indexes](#-indexes)
33. [Subqueries](#-subqueries)
34. [GROUP BY and HAVING](#-group-by-and-having)
35. [ROLLUP](#-rollup)
36. [Stored Procedures](#-stored-procedures)
37. [Triggers](#-triggers)
38. [Summary](#-summary)

---

## 🧠 What is a Database?

A **database** is a structured collection of data that can be stored, organized, and retrieved efficiently.
It helps users manage data easily using a **Database Management System (DBMS)** like MySQL.

---

## 📦 What is NoSQL?

**NoSQL** databases are used for storing **unstructured or semi-structured data**.
They are non-relational and great for big data and real-time applications.
Examples: **MongoDB, Redis, Cassandra, Firebase**.

---

## 👤 Creating a User and Granting Privileges

These commands create a new MySQL user and grant full access to all databases.

```sql
CREATE USER 'akhil'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'akhil'@'localhost' WITH GRANT OPTION;
```

---

## 🏗️ Creating and Using a Database

A **database** holds all your tables, views, and stored procedures.

```sql
CREATE DATABASE akhil;
USE akhil;
```

---

## 🧩 Creating a Table

A **table** stores data in rows and columns. Each column has a datatype and may include constraints.

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    gender ENUM('Male','Female','Other'),
    date_of_birth DATE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## 🔍 Selecting Data

Used to retrieve data from a table.

```sql
SELECT * FROM users;
```

---

## 🗑️ Dropping a Database

Completely deletes a database and all its data.

```sql
DROP DATABASE akhil;
```

---

## 🔑 Logging into the Database

Used to connect to a MySQL database via the terminal.

```bash
mysql -uakhil -ppassword akhil
```

---

## 🐳 Running SQL Scripts in Docker

Run `.sql` scripts inside a Docker MySQL container.

```bash
vi sqlscript.sql
docker compose cp sqlscript.sql openmrsdb:/
docker compose exec -it openmrsdb sh
mysql -uakhil -ppassword </sqlscript.sql
```

---

## 📄 sqlscript.sql Example

```sql
create database akhil;
USE akhil;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    gender ENUM('Male','Female','Other'),
    date_of_birth DATE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

SELECT * FROM users;
```

---

## 🧱 Datatypes and Constraints

**Datatypes** specify what type of data a column can store.
**Constraints** enforce rules on data.

```sql
SELECT name, email FROM users;
```

---

## ✏️ Renaming a Table

Rename an existing table.

```sql
RENAME TABLE users TO programmers;
```

---

## ⚙️ Altering a Table

Used to change a table’s structure.

### ➕ Add a Column

```sql
ALTER TABLE programmers ADD COLUMN is_active BOOLEAN DEFAULT true;
```

### ❌ Drop a Column

```sql
ALTER TABLE programmers DROP COLUMN is_active;
```

### 🔄 Modify a Column Type

```sql
ALTER TABLE programmers MODIFY COLUMN name VARCHAR(150);
```

### ⬆️ Reorder Columns

```sql
ALTER TABLE programmers MODIFY COLUMN email VARCHAR(100) AFTER id;
ALTER TABLE programmers MODIFY COLUMN date_of_birth DATETIME FIRST;
```

---

## 🧠 Inserting Data

Insert new records into a table.

```sql
INSERT INTO programmers VALUES
('1996-08-01',1,'akhilantotharayil@gmail.com','AKHIL','Male',DEFAULT),
('2002-12-17',2,'rushilantotharayil@gmail.com','Rushil','Male',DEFAULT),
('2001-08-21',3,'pmohite@gmail.com','Pranavi','Female',DEFAULT),
('1996-11-16',3,'syadav@gmail.com','Sandeepkumar','Male',DEFAULT),
('1996-10-02',4,'rgupta@gmail.com','Ritesh','Male',DEFAULT),
('1997-12-15',5,'ksayyed@gmail.com','Kaunian','Female',DEFAULT),
('1999-08-24',6,'staldevkar@gmail.com','Sunny','Male',DEFAULT);
```

---

## 🔎 Querying Data

Retrieve specific data using conditions.

```sql
SELECT * FROM users WHERE gender = 'Male';
```

---

## 🧾 Updating Data

Modify existing records.

```sql
UPDATE programmers
SET date_of_birth = '2021-09-01', email = 'atharayil@iplit.in', name = 'Akhil IPLit'
WHERE id = 2;
```

---

## 🗑️ Deleting Data

Remove records from a table.

```sql
DELETE FROM programmers WHERE name = 'Pranavi';
```

---

## 💥 Dropping a Table

Permanently remove a table.

```sql
DROP TABLE users;
```

---

## 🔐 Constraints in Detail

Constraints ensure data accuracy.
Examples: **PRIMARY KEY**, **FOREIGN KEY**, **NOT NULL**, **UNIQUE**, **CHECK**, **DEFAULT**

---

## 🧰 MySQL Functions

Useful built-in operations.

```sql
SELECT COUNT(*) FROM programmers;
SELECT MIN(date_of_birth), MAX(date_of_birth) FROM programmers;
SELECT name, LENGTH(name) AS name_len FROM users;
```

---

## ➕ Mathematical Functions

Perform numeric calculations.

```sql
SELECT salary, ROUND(salary), FLOOR(salary), CEIL(salary) FROM programmers;
```

---

## 💼 Adding Columns and UUIDs

Add columns and generate UUIDs for rows.

```sql
ALTER TABLE programmers
ADD COLUMN salary DECIMAL(10,2) AFTER gender,
ADD COLUMN uuid CHAR(36) AFTER salary;

UPDATE programmers SET uuid = UUID();
```

---

## 🔢 MOD, LOWER, UPPER, CONCAT

Mathematical and string functions.

```sql
SELECT id, MOD(id,2) AS remainder FROM programmers;
```

---

## 🧍‍♂️ Copying Table Structure and Data

Duplicate tables and their contents.

```sql
CREATE TABLE users LIKE programmers;
INSERT INTO users SELECT * FROM programmers;
```

---

## 🔄 Transactions

Used to ensure data consistency with **COMMIT** and **ROLLBACK**.

```sql
SET autocommit = 0;
SELECT * FROM users;
COMMIT;
DELETE FROM users WHERE id = 6;
ROLLBACK;
SET autocommit = 1;
```

---

## 🔑 Primary Key and Auto Increment

Uniquely identifies rows and auto-generates numeric IDs.

---

## 🔗 Foreign Keys

Used to link data between tables.

```sql
CREATE TABLE addresses (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    street VARCHAR(255),
    city VARCHAR(100),
    state VARCHAR(100),
    pincode VARCHAR(10),
    CONSTRAINT fk_user FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

---

## 🔀 MySQL Joins

Combine data from multiple tables.

### INNER JOIN

```sql
SELECT users.name, users.gender, addresses.city, addresses.state
FROM users
INNER JOIN addresses ON users.id = addresses.user_id;
```

---

## 🔂 UNION and UNION ALL

Combine results of two or more SELECT statements.

```sql
SELECT name FROM users
UNION
SELECT name FROM admin_users;

SELECT name FROM users
UNION ALL
SELECT name FROM admin_users;
```

---

## 🔁 SELF JOIN

Join a table with itself to compare related rows.

---

## 👁️ Views

A **View** is a saved SQL query that acts as a virtual table.

```sql
CREATE VIEW rich_users AS
SELECT * FROM users WHERE salary > 70000;

SELECT * FROM rich_users;
```

---

## 📇 Indexes

Indexes speed up query performance.

```sql
CREATE INDEX idx_email ON users(gender);
SHOW INDEXES FROM users;
DROP INDEX idx_email ON users;
```

---

## 🧩 Subqueries

Queries inside other queries.

```sql
SELECT * FROM users WHERE salary > (SELECT AVG(salary) FROM users);
```

---

## 📊 GROUP BY and HAVING

Used to group data and apply aggregate functions.

```sql
SELECT gender, AVG(salary) AS 'Average Salary', COUNT(*) AS 'Count'
FROM users
GROUP BY gender;

SELECT referred_by_id, COUNT(*) AS total_referred
FROM users
WHERE referred_by_id IS NOT NULL
GROUP BY referred_by_id
HAVING COUNT(*) > 1;
```

---

## 📈 ROLLUP

Provides subtotals and grand totals in grouped results.

```sql
SELECT gender, COUNT(*) AS total_users
FROM users
GROUP BY gender WITH ROLLUP;
```

---

## ⚙️ Stored Procedures

Reusable SQL code stored in the database.

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

## 🧾 Triggers

Automatically perform actions when an event occurs (e.g., after an INSERT).

### Create Log Table

```sql
CREATE TABLE user_log (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    name VARCHAR(100),
    created_on TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Create Trigger

```sql
DELIMITER $$
CREATE TRIGGER after_user_insert
AFTER INSERT ON users
FOR EACH ROW
BEGIN
    INSERT INTO user_log(user_id, name)
    VALUES(NEW.id, NEW.name);
END $$
DELIMITER ;
```

### Test Trigger

```sql
INSERT INTO users (name, email, gender, date_of_birth, salary)
VALUES ('Rohan','rohan@rohan.com','Male','2007-04-04',56000);
```

---

## ✅ Summary

This guide covers all MySQL essentials:

* Creating users and databases
* Table creation and manipulation
* CRUD operations
* Joins, Views, Subqueries
* Transactions and Triggers
* Indexes and Constraints

---

**Author:** Akhil Anto Tharayil
**Purpose:** MySQL Complete Notes for Hands-on Practice 💻

---


