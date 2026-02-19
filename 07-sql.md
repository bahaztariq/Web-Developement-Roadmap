# 🗄️ SQL - Structured Query Language

## Summary

This document covers SQL (Structured Query Language) for managing relational databases. Topics include database and table management (DDL), CRUD operations (DML), filtering and sorting, aggregate functions and grouping, various types of joins, subqueries, set operations, constraints and keys, indexing for performance optimization, views and stored procedures, transactions with ACID properties, database design and normalization, and advanced features like window functions and CTEs.

## Sommaire

- [1. Introduction to SQL](#1-introduction-to-sql)
  - [Definition](#definition)
  - [Database Architecture Overview](#database-architecture-overview)
  - [SQL Statement Categories (UML Classification)](#sql-statement-categories-uml-classification)
  - [Relational Databases](#relational-databases)
  - [SQL Categories](#sql-categories)
- [2. Database & Table Management (DDL)](#2-database-&-table-management-ddl)
  - [Definition](#definition)
  - [CREATE DATABASE](#create-database)
  - [CREATE TABLE](#create-table)
  - [Data Types](#data-types)
  - [ALTER TABLE](#alter-table)
  - [DROP and TRUNCATE](#drop-and-truncate)
- [3. CRUD Operations (DML)](#3-crud-operations-dml)
  - [Definition](#definition)
  - [INSERT](#insert)
  - [SELECT](#select)
  - [UPDATE](#update)
  - [DELETE](#delete)
  - [Basic WHERE Clause](#basic-where-clause)
- [4. Filtering & Sorting](#4-filtering-&-sorting)
  - [Definition](#definition)
  - [WHERE with Operators](#where-with-operators)
  - [AND / OR / NOT](#and-/-or-/-not)
  - [ORDER BY](#order-by)
  - [LIMIT / OFFSET](#limit-/-offset)
  - [DISTINCT](#distinct)
- [5. Functions & Aggregation](#5-functions-&-aggregation)
  - [Definition](#definition)
  - [Aggregate Functions](#aggregate-functions)
  - [GROUP BY](#group-by)
  - [HAVING](#having)
  - [String Functions](#string-functions)
  - [Date Functions](#date-functions)
  - [CASE WHEN](#case-when)
- [6. Joins](#6-joins)
  - [Definition](#definition)
  - [Join Types Visualization](#join-types-visualization)
  - [Venn Diagram Representation](#venn-diagram-representation)
  - [Join Types Reference](#join-types-reference)
  - [INNER JOIN](#inner-join)
  - [LEFT JOIN](#left-join)
  - [RIGHT JOIN](#right-join)
  - [FULL OUTER JOIN](#full-outer-join)
  - [CROSS JOIN](#cross-join)
  - [Self Join](#self-join)
  - [Multiple Joins](#multiple-joins)
- [7. Subqueries](#7-subqueries)
  - [Definition](#definition)
  - [Subqueries in WHERE](#subqueries-in-where)
  - [Subqueries in SELECT](#subqueries-in-select)
  - [Subqueries in FROM](#subqueries-in-from)
  - [Subqueries in INSERT/UPDATE/DELETE](#subqueries-in-insert/update/delete)
- [8. Set Operations](#8-set-operations)
  - [Definition](#definition)
  - [Set Operations Visualization](#set-operations-visualization)
  - [UNION](#union)
  - [UNION ALL](#union-all)
  - [INTERSECT](#intersect)
  - [EXCEPT / MINUS](#except-/-minus)
- [9. Constraints & Keys](#9-constraints-&-keys)
  - [Definition](#definition)
  - [PRIMARY KEY](#primary-key)
  - [FOREIGN KEY](#foreign-key)
  - [UNIQUE Constraint](#unique-constraint)
  - [NOT NULL & DEFAULT](#not-null-&-default)
  - [CHECK Constraint](#check-constraint)
  - [AUTO_INCREMENT / SERIAL](#auto_increment-/-serial)
- [10. Indexes](#10-indexes)
  - [Definition](#definition)
  - [Index B-Tree Structure](#index-b-tree-structure)
  - [CREATE INDEX](#create-index)
  - [Index Management](#index-management)
  - [EXPLAIN](#explain)
  - [Query Optimization Flow](#query-optimization-flow)
  - [When to Use Indexes](#when-to-use-indexes)
- [11. Views, Procedures & Triggers](#11-views-procedures-&-triggers)
  - [Definition](#definition)
  - [CREATE VIEW](#create-view)
  - [Stored Procedures](#stored-procedures)
  - [Triggers](#triggers)
- [12. Transactions](#12-transactions)
  - [Definition](#definition)
  - [Transaction ACID Properties](#transaction-acid-properties)
  - [Basic Transaction Control](#basic-transaction-control)
  - [Savepoints](#savepoints)
  - [ACID Properties](#acid-properties)
  - [Isolation Levels](#isolation-levels)
  - [Error Handling](#error-handling)
- [13. Database Design](#13-database-design)
  - [Definition](#definition)
  - [Entity-Relationship Diagram (ERD)](#entity-relationship-diagram-erd)
  - [Table Relationship Types](#table-relationship-types)
  - [Normalization Levels](#normalization-levels)
  - [Normalization](#normalization)
  - [Relationships](#relationships)
  - [ERD (Entity-Relationship Diagram)](#erd-entity-relationship-diagram)
- [14. Advanced Topics](#14-advanced-topics)
  - [Definition](#definition)
  - [SQL Execution Flow](#sql-execution-flow)
  - [Window Functions](#window-functions)
  - [CTEs (Common Table Expressions)](#ctes-common-table-expressions)
- [🔑 Key Takeaways](#🔑-key-takeaways)



> The standard language for relational database management systems. SQL is used to store, retrieve, update, and manage data.

---

## 1. Introduction to SQL

### Definition
SQL (Structured Query Language) is a standardized programming language for managing and manipulating relational databases. It enables users to create, read, update, and delete (CRUD) data, as well as define database schemas and relationships.

### Database Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                    APPLICATION LAYER                        │
│         (Web Apps, Mobile Apps, BI Tools, etc.)             │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    SQL INTERFACE                            │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐    │
│  │   DDL    │  │   DML    │  │   DQL    │  │   DCL    │    │
│  │ (Schema) │  │ (Modify) │  │ (Query)  │  │ (Access) │    │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘    │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│              RELATIONAL DATABASE MANAGEMENT SYSTEM          │
│  ┌─────────────────────────────────────────────────────┐   │
│  │              QUERY PROCESSOR                        │   │
│  │  Parser → Optimizer → Execution Plan → Executor     │   │
│  └─────────────────────────────────────────────────────┘   │
│  ┌─────────────────────────────────────────────────────┐   │
│  │              STORAGE ENGINE                         │   │
│  │  Tables • Indexes • Views • Transactions • Logs     │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    PHYSICAL STORAGE                         │
│         (Disks, SSDs, Memory Buffers, Files)                │
└─────────────────────────────────────────────────────────────┘
```

### SQL Statement Categories (UML Classification)

```
                           ┌─────────────────────┐
                           │      SQL COMMAND    │
                           └─────────────────────┘
                                    │
        ┌───────────────────────────┼───────────────────────────┐
        │                           │                           │
        ▼                           ▼                           ▼
┌───────────────┐         ┌─────────────────┐         ┌─────────────────┐
│     DDL       │         │      DML        │         │      DCL        │
│  (Data Def.)  │         │  (Data Manip.)  │         │ (Data Control)  │
└───────────────┘         └─────────────────┘         └─────────────────┘
        │                           │                           │
   ┌────┴────┐                 ┌────┴────┐                 ┌────┴────┐
   │         │                 │         │                 │         │
   ▼         ▼                 ▼         ▼                 ▼         ▼
CREATE    DROP             INSERT    UPDATE             GRANT    REVOKE
ALTER   TRUNCATE           DELETE    MERGE

                           ┌─────────────────┐
                           │      DQL        │
                           │  (Data Query)   │
                           └─────────────────┘
                                   │
                                   ▼
                              SELECT
```

### Relational Databases
Relational databases organize data into tables (relations) with rows (records) and columns (fields). Tables can be related to each other through keys.

**Popular SQL Databases:**

| Database | Best For |
|----------|----------|
| MySQL | Web applications, small-to-medium projects |
| PostgreSQL | Complex queries, advanced features, enterprise |
| SQLite | Mobile apps, embedded systems, testing |
| SQL Server | Microsoft environments, enterprise solutions |
| Oracle | Large-scale enterprise applications |

### SQL Categories

| Category | Commands | Purpose |
|----------|----------|---------|
| **DDL** | CREATE, ALTER, DROP, TRUNCATE | Define database structure |
| **DML** | INSERT, UPDATE, DELETE | Manipulate data |
| **DQL** | SELECT | Query data |
| **DCL** | GRANT, REVOKE | Control access |
| **TCL** | COMMIT, ROLLBACK, SAVEPOINT | Manage transactions |

---

## 2. Database & Table Management (DDL)

### Definition
**DDL (Data Definition Language)** commands define and manage the structure of database objects. These commands create, modify, and remove database schemas, tables, indexes, and constraints. DDL operations are auto-committed and cannot be rolled back in most database systems.

### CREATE DATABASE

**Definition:** The `CREATE DATABASE` statement creates a new database container. It is the first step in setting up a new project. You typically check if it exists first (`IF NOT EXISTS`) to verify the command is idempotent.

```sql
-- Create a new database
CREATE DATABASE myapp;

-- Create database with character set (MySQL)
CREATE DATABASE myapp
    CHARACTER SET utf8mb4
    COLLATE utf8mb4_unicode_ci;

-- Use the database
USE myapp;
```

### CREATE TABLE

```sql
-- Create a basic table
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(100) NOT NULL,
    age INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Create table with constraints
CREATE TABLE orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    total_amount DECIMAL(10, 2) NOT NULL,
    order_date DATE NOT NULL,
    status ENUM('pending', 'processing', 'shipped', 'delivered') DEFAULT 'pending',
    -- Foreign key constraint
    FOREIGN KEY (user_id) REFERENCES users(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);
```

### Data Types

**Definition:** SQL requires every column to have a defined data type. Choosing the correct type is critical for storage efficiency and data integrity.

| Category | Type | Description |
|----------|------|-------------|
| **Numeric** | `INT` / `INTEGER` | Whole numbers (-2.1B to 2.1B) |
| | `BIGINT` | Large whole numbers |
| | `DECIMAL(p,s)` | Exact precision (currency) |
| | `FLOAT` / `DOUBLE` | Approximate decimal numbers |
| **String** | `CHAR(n)` | Fixed-length strings |
| | `VARCHAR(n)` | Variable-length strings |
| | `TEXT` | Large text data |
| **Date/Time** | `DATE` | Date only (YYYY-MM-DD) |
| | `TIME` | Time only (HH:MM:SS) |
| | `DATETIME` | Date and time |
| | `TIMESTAMP` | Unix timestamp (auto-updates) |
| **Binary** | `BLOB` | Binary large objects (images, files) |
| **Others** | `BOOLEAN` | True/False values |
| | `JSON` | JSON data structures |
| | `UUID` | Universally Unique Identifiers |


### ALTER TABLE

```sql
-- Add a column
ALTER TABLE users
    ADD phone VARCHAR(20);

-- Add column with position (MySQL)
ALTER TABLE users
    ADD middle_name VARCHAR(50) AFTER first_name;

-- Modify column
ALTER TABLE users
    MODIFY phone VARCHAR(30);

-- Rename column (MySQL 8.0+)
ALTER TABLE users
    RENAME COLUMN phone TO phone_number;

-- Drop a column
ALTER TABLE users
    DROP COLUMN phone_number;

-- Add index
ALTER TABLE users
    ADD INDEX idx_email (email);

-- Add foreign key
ALTER TABLE orders
    ADD CONSTRAINT fk_user
    FOREIGN KEY (user_id) REFERENCES users(id);

-- Drop foreign key
ALTER TABLE orders
    DROP FOREIGN KEY fk_user;
```

### DROP and TRUNCATE

**Definition:** `DROP TABLE` removes the table definition and all its data permanently from the database. `TRUNCATE TABLE` removes all rows from the table but keeps the table structure (schema) intact, essentially resetting it. `TRUNCATE` is faster than `DELETE` but cannot be rolled back in some SQL dialects.

```sql
-- Delete table completely (structure and data)
DROP TABLE IF EXISTS temp_table;

-- Delete all data but keep table structure
TRUNCATE TABLE temp_table;

-- Delete database
DROP DATABASE IF EXISTS old_database;
```

**Best Practices:**
- Always use `IF EXISTS` to avoid errors
- Use `TRUNCATE` instead of `DELETE` without WHERE for better performance
- Backup before dropping tables/databases
- Name constraints explicitly (for easier removal)

---

## 3. CRUD Operations (DML)

### Definition
**DML (Data Manipulation Language)** commands manage data within existing database objects. CRUD stands for Create, Read, Update, Delete—the four basic operations for persistent storage. DML operations can be rolled back when wrapped in transactions.

### INSERT

**Definition:** The `INSERT INTO` statement adds new rows of data to a table. You can insert values into specific columns (specifying column names is best practice) or all columns. Bulk inserts allow adding multiple rows in a single query for better performance.

```sql
-- Insert single row
INSERT INTO users (username, email, age)
VALUES ('john_doe', 'john@example.com', 28);

-- Insert multiple rows
INSERT INTO users (username, email, age) VALUES
    ('jane_doe', 'jane@example.com', 32),
    ('bob_smith', 'bob@example.com', 45),
    ('alice_jones', 'alice@example.com', 29);

-- Insert with SELECT (copy data)
INSERT INTO users_archive (username, email, age)
SELECT username, email, age
FROM users
WHERE is_active = FALSE;

-- Insert or update (MySQL - INSERT ... ON DUPLICATE KEY)
INSERT INTO users (id, username, email)
VALUES (1, 'john_doe', 'john.new@example.com')
ON DUPLICATE KEY UPDATE
    email = VALUES(email),
    updated_at = CURRENT_TIMESTAMP;

-- Insert or ignore (MySQL)
INSERT IGNORE INTO users (username, email)
VALUES ('john_doe', 'john@example.com');
```

### SELECT

**Definition:** The `SELECT` statement retrieves data from a database. It allows you to specify exactly which columns to return (`SELECT col1, col2`) or all columns (`SELECT *`). It is the foundation of specific data retrieval and is usually accompanied by `FROM` to specify the source table.

```sql
-- Select all columns
SELECT * FROM users;

-- Select specific columns
SELECT username, email, age FROM users;

-- Select with alias
SELECT 
    username AS user_name,
    email AS user_email,
    age AS user_age
FROM users;

-- Select with calculated column
SELECT 
    username,
    email,
    age,
    age * 12 AS age_in_months
FROM users;

-- Select unique values
SELECT DISTINCT country FROM users;
```

### UPDATE

**Definition:** The `UPDATE` statement modifies existing data in a table. It is almost always used with a `WHERE` clause to target specific rows. Without a `WHERE` clause, **all rows** in the table will be updated.

```sql
-- Update single column
UPDATE users
SET is_active = FALSE
WHERE id = 5;

-- Update multiple columns
UPDATE users
SET 
    email = 'newemail@example.com',
    age = 29,
    updated_at = CURRENT_TIMESTAMP
WHERE id = 5;

-- Update with calculation
UPDATE products
SET price = price * 1.10  -- Increase prices by 10%
WHERE category = 'electronics';

-- Update with join
UPDATE users u
JOIN orders o ON u.id = o.user_id
SET u.last_order_date = o.order_date
WHERE o.status = 'delivered';

-- WARNING: Always use WHERE with UPDATE!
-- Without WHERE, ALL rows will be updated
```

### DELETE

**Definition:** The `DELETE` statement removes existing rows from a table. Like `UPDATE`, it is typically used with a `WHERE` clause to target specific records. Without a `WHERE` clause, **all rows** are deleted, similar to `TRUNCATE` but slower and logged transactionally.

```sql
-- Delete specific rows
DELETE FROM users
WHERE id = 5;

-- Delete with condition
DELETE FROM users
WHERE is_active = FALSE 
  AND last_login < DATE_SUB(CURRENT_DATE, INTERVAL 1 YEAR);

-- Delete with limit
DELETE FROM logs
WHERE created_at < DATE_SUB(NOW(), INTERVAL 30 DAY)
LIMIT 1000;

-- Delete with join
DELETE u FROM users u
JOIN orders o ON u.id = o.user_id
WHERE o.order_count = 0;

-- WARNING: Always use WHERE with DELETE!
-- Without WHERE, ALL rows will be deleted
```

### Basic WHERE Clause

**Definition:** The `WHERE` clause filters records based on specified conditions. It follows the `FROM` clause in a `SELECT`, `UPDATE`, or `DELETE` statement. Only rows that satisfy the condition (evaluate to TRUE) are included in the result or affected by the operation.

```sql
-- Equality
SELECT * FROM users WHERE age = 25;

-- Inequality
SELECT * FROM users WHERE age != 25;
SELECT * FROM users WHERE age <> 25;

-- Comparison operators
SELECT * FROM users WHERE age > 18;    -- Greater than
SELECT * FROM users WHERE age < 65;    -- Less than
SELECT * FROM users WHERE age >= 21;   -- Greater or equal
SELECT * FROM users WHERE age <= 30;   -- Less or equal

-- NULL checks
SELECT * FROM users WHERE phone IS NULL;
SELECT * FROM users WHERE phone IS NOT NULL;
```

**Best Practices:**
- Always use `WHERE` with `UPDATE` and `DELETE`
- Test `SELECT` first before running `UPDATE` or `DELETE`
- Use transactions for batch operations
- Limit large deletes with `LIMIT` clause

---

## 4. Filtering & Sorting

### Definition
Filtering and sorting operations refine query results to return only relevant data in a specific order. Filtering uses the WHERE clause with conditions, while sorting uses ORDER BY. These operations are essential for data presentation and analysis, allowing users to focus on specific subsets of data.

### WHERE with Operators

**Definition:** SQL supports standard comparison operators in the `WHERE` clause: `=` (equal), `<>` or `!=` (not equal), `>` (greater than), `<` (less than), `>=` (greater or equal), `<=` (less or equal). These allow for precise filtering logic.

```sql
-- LIKE (pattern matching)
SELECT * FROM users WHERE username LIKE 'john%';   -- Starts with 'john'
SELECT * FROM users WHERE username LIKE '%doe';    -- Ends with 'doe'
SELECT * FROM users WHERE username LIKE '%smith%'; -- Contains 'smith'
SELECT * FROM users WHERE username LIKE 'j_n%';    -- 'j', any char, 'n', then anything

-- ESCAPE for special characters
SELECT * FROM products WHERE description LIKE '%50%%' ESCAPE '%';  -- Finds '50%'

-- BETWEEN (inclusive range)
SELECT * FROM products WHERE price BETWEEN 10 AND 50;
SELECT * FROM users WHERE birth_date BETWEEN '1990-01-01' AND '1999-12-31';

-- IN (match any value in list)
SELECT * FROM users WHERE country IN ('USA', 'UK', 'Canada');
SELECT * FROM orders WHERE status IN ('pending', 'processing');

-- NOT IN
SELECT * FROM products WHERE category NOT IN ('electronics', 'clothing');
```

### AND / OR / NOT

**Definition:** Logical operators combine multiple conditions in a `WHERE` clause. `AND` requires both conditions to be true. `OR` requires at least one condition to be true. `NOT` negates a condition. Parentheses `()` should be used to explicitly group conditions and control evaluation order.

```sql
-- AND (all conditions must be true)
SELECT * FROM users 
WHERE age >= 18 
  AND country = 'USA' 
  AND is_active = TRUE;

-- OR (any condition can be true)
SELECT * FROM users 
WHERE country = 'USA' 
   OR country = 'Canada' 
   OR country = 'UK';

-- Combining AND and OR (use parentheses!)
SELECT * FROM users 
WHERE (country = 'USA' OR country = 'Canada')
  AND age >= 18;

-- NOT (negation)
SELECT * FROM users WHERE NOT age < 18;
SELECT * FROM users WHERE NOT country = 'USA';
```

### ORDER BY

**Definition:** The `ORDER BY` clause sorts the result set by one or more columns in ascending (`ASC`, default) or descending (`DESC`) order. It is the last clause processed in a SELECT statement (before LIMIT).

```sql
-- Ascending order (default)
SELECT * FROM users ORDER BY username ASC;

-- Descending order
SELECT * FROM users ORDER BY age DESC;

-- Multiple columns
SELECT * FROM users 
ORDER BY country ASC, age DESC;

-- Order by column position
SELECT username, email, age FROM users ORDER BY 3 DESC;  -- Order by 3rd column (age)

-- Order with NULL handling (MySQL)
SELECT * FROM users ORDER BY phone IS NULL, phone;  -- NULLs last
```

### LIMIT / OFFSET

**Definition:** `LIMIT` restricts the number of rows returned by the query. `OFFSET` skips a specified number of rows before returning the result. Together, they are the standard mechanism for implementing pagination in applications.

```sql
-- MySQL / PostgreSQL
SELECT * FROM users LIMIT 10;                    -- First 10 rows
SELECT * FROM users LIMIT 10 OFFSET 20;          -- Rows 21-30
SELECT * FROM users LIMIT 20, 10;                -- MySQL: offset 20, limit 10

-- SQL Server
SELECT TOP 10 * FROM users;
SELECT TOP 10 * FROM users ORDER BY id;  -- With ordering

-- Oracle
SELECT * FROM users WHERE ROWNUM <= 10;

-- Pagination example (page 3, 10 items per page)
SELECT * FROM users
ORDER BY id
LIMIT 10 OFFSET 20;  -- Skip 20, show 10
```

### DISTINCT

**Definition:** The `DISTINCT` keyword eliminates duplicate rows from the result set, returning only unique values. It operates on the entire row selected, so `SELECT DISTINCT col1, col2` ensures the *combination* of col1 and col2 is unique.

```sql
-- Unique values in one column
SELECT DISTINCT country FROM users;

-- Unique combinations
SELECT DISTINCT country, city FROM users;

-- Count unique values
SELECT COUNT(DISTINCT country) FROM users;
```

**Best Practices:**
- Use indexes on frequently filtered columns
- Place most selective conditions first in WHERE
- Use `EXPLAIN` to check query performance
- Avoid functions on indexed columns in WHERE clauses

---

## 5. Functions & Aggregation

### Definition
Functions and aggregation perform calculations and transformations on data. Aggregate functions summarize multiple rows into single values (COUNT, SUM, AVG, etc.), while scalar functions manipulate individual values (string, date, numeric functions). GROUP BY organizes data into groups for aggregation, and HAVING filters these groups.

### Aggregate Functions

**Definition:** Aggregate functions perform a calculation on a set of values (a column) and return a single scalar value. Common functions include `COUNT()` (number of rows), `SUM()` (total), `AVG()` (average), `MIN()` (minimum), and `MAX()` (maximum). They ignore NULL values (except `COUNT(*)`).

```sql
-- COUNT
SELECT COUNT(*) FROM users;                    -- Count all rows
SELECT COUNT(id) FROM users;                   -- Count non-NULL ids
SELECT COUNT(DISTINCT country) FROM users;     -- Count unique countries

-- SUM
SELECT SUM(price) FROM orders;
SELECT SUM(price * quantity) AS total_revenue FROM order_items;

-- AVG
SELECT AVG(age) FROM users;
SELECT AVG(price) AS avg_price FROM products WHERE category = 'electronics';

-- MIN / MAX
SELECT MIN(price), MAX(price), AVG(price) FROM products;
SELECT MIN(order_date), MAX(order_date) FROM orders;

-- Combined example
SELECT 
    category,
    COUNT(*) AS product_count,
    MIN(price) AS min_price,
    MAX(price) AS max_price,
    AVG(price) AS avg_price,
    SUM(stock_quantity) AS total_stock
FROM products
GROUP BY category;
```

### GROUP BY

**Definition:** The `GROUP BY` clause groups rows that have the same values in specified columns into summary rows. It is almost always used with aggregate functions to perform calculations on each group (e.g., "count users per country").

```sql
-- Group by single column
SELECT country, COUNT(*) AS user_count
FROM users
GROUP BY country;

-- Group by multiple columns
SELECT country, city, COUNT(*) AS user_count
FROM users
GROUP BY country, city;

-- Group with expression
SELECT YEAR(created_at) AS year, COUNT(*) AS count
FROM users
GROUP BY YEAR(created_at);

-- Group with aggregate functions
SELECT 
    category,
    COUNT(*) AS product_count,
    AVG(price) AS avg_price
FROM products
GROUP BY category
ORDER BY avg_price DESC;
```

### HAVING

**Definition:** The `HAVING` clause filters groups created by `GROUP BY`. Unlike `WHERE` (which filters individual rows *before* grouping), `HAVING` filters the aggregated results *after* grouping. It allows conditions on aggregate functions (e.g., `HAVING COUNT(*) > 5`).

```sql
-- Filter groups (HAVING = WHERE for GROUP BY)
SELECT country, COUNT(*) AS user_count
FROM users
GROUP BY country
HAVING COUNT(*) > 100;

-- HAVING with multiple conditions
SELECT 
    category,
    AVG(price) AS avg_price,
    COUNT(*) AS product_count
FROM products
GROUP BY category
HAVING AVG(price) > 50
   AND COUNT(*) >= 10;

-- WHERE vs HAVING
SELECT category, AVG(price) AS avg_price
FROM products
WHERE is_active = TRUE        -- Filter rows before grouping
GROUP BY category
HAVING AVG(price) > 100;      -- Filter groups after grouping
```

### String Functions

**Definition:** SQL provides functions to manipulate text strings. Common functions include `CONCAT` (joins strings), `UPPER`/`LOWER` (case conversion), `SUBSTRING` (extracts parts), `LENGTH` (string length), and `TRIM` (removes whitespace). Syntax varies slightly between SQL dialects (MySQL vs PostgreSQL).

```sql
-- Concatenation
SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM users;
SELECT CONCAT_WS(' ', first_name, middle_name, last_name) FROM users;

-- Case conversion
SELECT UPPER(username), LOWER(email) FROM users;

-- Substring
SELECT SUBSTRING(email, 1, 5) FROM users;           -- First 5 chars
SELECT SUBSTRING(email FROM 1 FOR 5) FROM users;    -- ANSI SQL

-- Length
SELECT LENGTH(username), CHAR_LENGTH(username) FROM users;

-- Trim
SELECT TRIM('  hello  ');                    -- 'hello'
SELECT LTRIM('  hello');                     -- 'hello  '
SELECT RTRIM('hello  ');                     -- '  hello'
SELECT TRIM(BOTH 'x' FROM 'xxxhelloxxx');    -- 'hello'

-- Replace
SELECT REPLACE(email, '@gmail.com', '@company.com') FROM users;

-- Find position
SELECT POSITION('@' IN email) FROM users;
SELECT INSTR(email, '@') FROM users;  -- MySQL

-- Left / Right
SELECT LEFT(email, 5), RIGHT(email, 10) FROM users;

-- Formatting
SELECT FORMAT(price, 2) FROM products;        -- MySQL: 1234.5 -> '1,234.50'
```

### Date Functions

**Definition:** Date functions handle date and time values. They allow you to get the current date (`NOW()`, `CURRENT_DATE`), extract parts (`YEAR()`, `MONTH()`), add/subtract intervals (`DATE_ADD`), and format dates. Accurate date manipulation is crucial for reporting and scheduling.

```sql
-- Current date/time
SELECT CURRENT_DATE;
SELECT CURRENT_TIME;
SELECT CURRENT_TIMESTAMP;
SELECT NOW();           -- MySQL

-- Extract parts
SELECT YEAR(created_at), MONTH(created_at), DAY(created_at) FROM users;
SELECT HOUR(created_at), MINUTE(created_at), SECOND(created_at) FROM users;

-- Date arithmetic
SELECT DATE_ADD(CURRENT_DATE, INTERVAL 7 DAY);      -- Add 7 days
SELECT DATE_SUB(CURRENT_DATE, INTERVAL 1 MONTH);    -- Subtract 1 month
SELECT DATEDIFF(end_date, start_date);              -- Difference in days

-- Formatting
SELECT DATE_FORMAT(created_at, '%Y-%m-%d') FROM users;           -- MySQL
SELECT TO_CHAR(created_at, 'YYYY-MM-DD') FROM users;             -- PostgreSQL/Oracle

-- Other useful functions
SELECT LAST_DAY(CURRENT_DATE);                      -- Last day of month
SELECT DAYOFWEEK(CURRENT_DATE);                     -- Day of week (1=Sunday)
SELECT WEEK(CURRENT_DATE);                          -- Week number
```

### CASE WHEN

**Definition:** The `CASE` expression is SQL's way of handling if/then logic within a query. It goes through conditions sequentially and returns a value when the first condition is met. It is often used to create custom labels, pivot data, or handle conditional formatting directly in the database.

```sql
-- Simple CASE
SELECT 
    username,
    age,
    CASE 
        WHEN age < 18 THEN 'Minor'
        WHEN age BETWEEN 18 AND 65 THEN 'Adult'
        ELSE 'Senior'
    END AS age_group
FROM users;

-- CASE in aggregation
SELECT 
    COUNT(CASE WHEN status = 'active' THEN 1 END) AS active_users,
    COUNT(CASE WHEN status = 'inactive' THEN 1 END) AS inactive_users,
    COUNT(*) AS total_users
FROM users;

-- CASE for conditional aggregation
SELECT 
    category,
    SUM(CASE WHEN YEAR(order_date) = 2023 THEN amount ELSE 0 END) AS sales_2023,
    SUM(CASE WHEN YEAR(order_date) = 2024 THEN amount ELSE 0 END) AS sales_2024
FROM orders
GROUP BY category;

-- CASE for sorting
SELECT * FROM users
ORDER BY 
    CASE 
        WHEN priority = 'high' THEN 1
        WHEN priority = 'medium' THEN 2
        ELSE 3
    END;
```

**Best Practices:**
- Use indexes for columns in GROUP BY
- HAVING is less efficient than WHERE - filter early when possible
- Avoid functions on indexed columns in WHERE clauses
- Use COALESCE() to handle NULL values in calculations

---

## 6. Joins

### Definition
Joins combine rows from two or more tables based on related columns. They are fundamental to relational database queries, allowing data from normalized tables to be retrieved together. Joins eliminate the need for multiple queries and data manipulation in application code.

### Join Types Visualization

```
INNER JOIN (Intersection)
┌─────────────────────────────────────────┐
│              Table A                    │
│    ┌─────────────────────────┐          │
│    │   ░░░░░░░░░░░░░░░░░░   │          │
│    │   ░ MATCHING ROWS  ░   │          │
│    │   ░░░░░░░░░░░░░░░░░░   │          │
│    └─────────────────────────┘          │
│              Table B                    │
└─────────────────────────────────────────┘

LEFT JOIN (All from A + matching from B)
┌─────────────────────────────────────────┐
│              Table A                    │
│  ┌─────────────────────────────────┐    │
│  │ ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ │    │
│  │ ▓ ALL ROWS FROM LEFT TABLE  ▓ │    │
│  │ ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ │    │
│  └─────────────────────────────────┘    │
│              Table B                    │
└─────────────────────────────────────────┘

FULL OUTER JOIN (Union of both tables)
┌─────────────────────────────────────────┐
│              Table A                    │
│  ┌─────────────────────────────────┐    │
│  │ ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ │    │
│  │ ░ ALL FROM A + ALL FROM B   ░ │    │
│  │ ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ │    │
│  └─────────────────────────────────┘    │
│              Table B                    │
└─────────────────────────────────────────┘
```

### Venn Diagram Representation

```
        INNER JOIN              LEFT JOIN
    ┌─────────┐              ┌─────────┐
   /    ▓▓▓    \            /▓▓▓▓▓▓▓▓▓\
  ( A ▓▓▓▓▓ B )            (A▓▓▓▓▓  B )
   \    ▓▓▓    /            \▓▓▓▓▓    /
    └─────────┘              └─────────┘

      RIGHT JOIN             FULL JOIN
    ┌─────────┐              ┌─────────┐
   /    ▓▓▓▓▓\              /▓▓▓▓▓▓▓▓▓\
  ( A  ▓▓▓▓▓B▓)            (A▓▓▓▓▓▓▓▓B)
   \    ▓▓▓▓▓/              \▓▓▓▓▓▓▓▓▓/
    └─────────┘              └─────────┘
    
   ▓ = Included in result
```

### Join Types Reference

| Join Type | Description | Result Set |
|-----------|-------------|------------|
| `INNER JOIN` | Matches in both tables | Intersection (A ∩ B) |
| `LEFT JOIN` | All from Left + Matches from Right | Left table + matching Right rows |
| `RIGHT JOIN` | All from Right + Matches from Left | Right table + matching Left rows |
| `FULL OUTER JOIN` | Matches in either table | Union (A ∪ B) - All rows |
| `CROSS JOIN` | Cartesian product | Every row in A matched with every row in B |


### INNER JOIN

**Definition:** An `INNER JOIN` returns only the rows where there is a matching value in both joined tables. Rows with no match in either table are excluded from the result. It is the most common join type, used to retrieve related data that exists in both locations.

```sql
-- Basic inner join (returns matching rows only)
SELECT users.username, orders.order_id, orders.total_amount
FROM users
INNER JOIN orders ON users.id = orders.user_id;

-- Using aliases
SELECT u.username, o.order_id, o.total_amount
FROM users u
INNER JOIN orders o ON u.id = o.user_id;

-- Join with WHERE
SELECT u.username, o.order_id
FROM users u
INNER JOIN orders o ON u.id = o.user_id
WHERE o.total_amount > 100;

-- Join multiple tables
SELECT 
    u.username,
    o.order_id,
    p.product_name,
    oi.quantity
FROM users u
INNER JOIN orders o ON u.id = o.user_id
INNER JOIN order_items oi ON o.order_id = oi.order_id
INNER JOIN products p ON oi.product_id = p.product_id;

-- USING shorthand (when column names match)
SELECT u.username, o.order_id
FROM users u
INNER JOIN orders o USING (user_id);
```

### LEFT JOIN

**Definition:** A `LEFT JOIN` (or LEFT OUTER JOIN) returns all rows from the left table, and the matched rows from the right table. If there is no match, the result is NULL on the right side. It is used to include records even if they don't have related data (e.g., "show all users, even those without orders").

```sql
-- Left join (all from left table, matching from right)
SELECT u.username, o.order_id
FROM users u
LEFT JOIN orders o ON u.id = o.user_id;

-- Find users with no orders
SELECT u.username
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
WHERE o.order_id IS NULL;

-- Count orders per user (including users with 0 orders)
SELECT 
    u.username,
    COUNT(o.order_id) AS order_count
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
GROUP BY u.id, u.username;
```

### RIGHT JOIN

**Definition:** A `RIGHT JOIN` returns all rows from the right table, and the matched rows from the left table. It is the semantic opposite of LEFT JOIN. Most developers prefer using LEFT JOIN exclusively for consistency and readability.

```sql
-- Right join (all from right table, matching from left)
SELECT u.username, o.order_id
FROM users u
RIGHT JOIN orders o ON u.id = o.user_id;

-- Note: Right join is rarely used, typically just swap table order
-- and use LEFT JOIN instead
```

### FULL OUTER JOIN

**Definition:** A `FULL OUTER JOIN` returns all rows when there is a match in *either* the left or right table. If there is no match, the missing side will contain NULLs. It combines the results of both LEFT and RIGHT joins. (Note: MySQL does not support FULL JOIN directly; use UNION of LEFT and RIGHT joins).

```sql
-- Full join (all rows from both tables)
-- PostgreSQL, SQL Server, Oracle
SELECT u.username, o.order_id
FROM users u
FULL OUTER JOIN orders o ON u.id = o.user_id;

-- MySQL workaround (no FULL JOIN support)
SELECT u.username, o.order_id
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
UNION
SELECT u.username, o.order_id
FROM users u
RIGHT JOIN orders o ON u.id = o.user_id;
```

### CROSS JOIN

**Definition:** A `CROSS JOIN` produces the Cartesian product of two tables — pairing every row from the first table with every row from the second table. This results in N x M rows. It is rarely used in production except for generating combinations or seed data.

```sql
-- Cross join (Cartesian product - every combination)
SELECT u.username, p.product_name
FROM users u
CROSS JOIN products p;

-- Implicit cross join (comma syntax)
SELECT u.username, p.product_name
FROM users u, products p;

-- Use case: generate all combinations
SELECT 
    s.size,
    c.color,
    CONCAT(s.size, ' - ', c.color) AS variant
FROM sizes s
CROSS JOIN colors c;
```

### Self Join

**Definition:** A Self Join is a regular join where a table is joined to itself. This is useful for hierarchical data stored in a single table (e.g., retrieving an employee and their manager from an `employees` table). You must use table aliases to distinguish the two instances of the table.

```sql
-- Employees and their managers
SELECT 
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.employee_id;

-- Find pairs in same department
SELECT 
    e1.name AS employee1,
    e2.name AS employee2,
    e1.department
FROM employees e1
INNER JOIN employees e2 ON e1.department = e2.department
WHERE e1.employee_id < e2.employee_id;  -- Avoid duplicates
```

### Multiple Joins

**Definition:** You can chain multiple JOIN clauses in a single query to connect more than two tables. The database processes them in sequence (logically). This allows traversing complex relationships (e.g., generic User -> Order -> OrderItem -> Product).

```sql
-- Complex query with multiple joins
SELECT 
    c.customer_name,
    o.order_date,
    p.product_name,
    cat.category_name,
    oi.quantity,
    oi.price,
    (oi.quantity * oi.price) AS line_total,
    s.shipper_name
FROM customers c
INNER JOIN orders o ON c.customer_id = o.customer_id
INNER JOIN order_items oi ON o.order_id = oi.order_id
INNER JOIN products p ON oi.product_id = p.product_id
INNER JOIN categories cat ON p.category_id = cat.category_id
LEFT JOIN shippers s ON o.shipper_id = s.shipper_id
WHERE o.order_date >= '2024-01-01'
ORDER BY o.order_date DESC;
```

**Best Practices:**
- Use explicit JOIN syntax (avoid comma joins)
- Always specify join conditions (ON clause)
- Use aliases for readability
- Index foreign key columns for performance
- Start with the most restrictive table

---

## 7. Subqueries

### Definition
Subqueries (nested queries or inner queries) are queries embedded within other SQL statements. They can return scalar values, single rows, or multiple rows for use in the outer query's WHERE, FROM, SELECT, or HAVING clauses. Subqueries enable complex data retrieval without multiple round trips to the database.

### Subqueries in WHERE

**Definition:** A subquery in the `WHERE` clause allows filtering results based on the output of another query. It is often used with `IN`, `NOT IN`, `EXISTS`, or comparison operators (e.g., "Find users whose age is greater than the average age").

```sql
-- Subquery with IN
SELECT * FROM products
WHERE category_id IN (
    SELECT category_id 
    FROM categories 
    WHERE category_name IN ('Electronics', 'Books')
);

-- Subquery with comparison operator
SELECT * FROM employees
WHERE salary > (
    SELECT AVG(salary) FROM employees
);

-- Subquery with ALL/ANY
SELECT * FROM products
WHERE price > ALL (
    SELECT price FROM products WHERE category = 'discount'
);

-- Correlated subquery
SELECT * FROM employees e
WHERE salary > (
    SELECT AVG(salary) 
    FROM employees 
    WHERE department = e.department
);

-- EXISTS
SELECT * FROM customers c
WHERE EXISTS (
    SELECT 1 FROM orders o
    WHERE o.customer_id = c.customer_id
);

-- NOT EXISTS
SELECT * FROM customers c
WHERE NOT EXISTS (
    SELECT 1 FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

### Subqueries in SELECT

**Definition:** A subquery in the `SELECT` clause (scalar subquery) acts as a calculated column. It must return a single value (one row, one column) for each row of the main query. This is useful for adding a specific derived value (e.g., "count of orders") to the main result set.

```sql
-- Scalar subquery (returns single value)
SELECT 
    username,
    (SELECT COUNT(*) FROM orders WHERE user_id = u.id) AS order_count
FROM users u;

-- Calculate percentage
SELECT 
    category,
    COUNT(*) AS product_count,
    (COUNT(*) * 100.0 / (SELECT COUNT(*) FROM products)) AS percentage
FROM products
GROUP BY category;
```

### Subqueries in FROM

**Definition:** A subquery in the `FROM` clause (Derived Table) creates a temporary virtual table that the outer query can select from. Every derived table must have an alias. This is commonly used when you need to aggregate data first and then filter or join the aggregated results.

```sql
-- Derived table (subquery in FROM)
SELECT 
    department,
    AVG(salary) AS avg_salary
FROM (
    SELECT 
        department,
        salary
    FROM employees
    WHERE hire_date >= '2023-01-01'
) AS recent_hires
GROUP BY department;

-- Subquery with aggregate
SELECT avg_order.avg_amount
FROM (
    SELECT AVG(total_amount) AS avg_amount
    FROM orders
    WHERE order_date >= DATE_SUB(CURRENT_DATE, INTERVAL 30 DAY)
) AS avg_order;
```

### Subqueries in INSERT/UPDATE/DELETE

**Definition:** Subqueries can be used in DML statements to dynamically determine which rows to modify or what values to insert. For example, `INSERT INTO archive SELECT * FROM orders WHERE date < ...` moves old data efficiently.

```sql
-- INSERT with subquery
INSERT INTO top_customers (customer_id, total_spent)
SELECT 
    customer_id,
    SUM(total_amount)
FROM orders
GROUP BY customer_id
HAVING SUM(total_amount) > 10000;

-- UPDATE with subquery
UPDATE products p
SET price = price * 1.10
WHERE category_id IN (
    SELECT category_id
    FROM categories
    WHERE category_name = 'Premium'
);

-- DELETE with subquery
DELETE FROM users
WHERE id NOT IN (
    SELECT DISTINCT user_id 
    FROM orders 
    WHERE order_date >= DATE_SUB(CURRENT_DATE, INTERVAL 1 YEAR)
);
```

**Best Practices:**
- Use JOINs instead of subqueries when possible (usually faster)
- Ensure subqueries return appropriate number of rows
- Correlated subqueries can be slow on large datasets
- Use EXISTS instead of IN for large datasets
- Consider using CTEs (WITH clause) for complex subqueries

---

## 8. Set Operations

### Definition
Set operations combine the results of two or more SELECT queries into a single result set. These operations follow mathematical set theory principles: UNION combines results, INTERSECT returns common rows, and EXCEPT/MINUS returns differences. All queries must have compatible column types and the same number of columns.

### Set Operations Visualization

```
UNION (All unique rows from both)
┌────────────────────────────────────────┐
│              Table A                   │
│         ┌──────────────┐               │
│        /   ▓▓▓▓▓▓▓▓▓   \              │
│       (  A ▓▓▓▓▓▓▓ B  )               │
│        \   ▓▓▓▓▓▓▓▓▓   /              │
│         └──────────────┘               │
│              Table B                   │
└────────────────────────────────────────┘

INTERSECT (Only common rows)
┌────────────────────────────────────────┐
│              Table A                   │
│         ┌──────────────┐               │
│        /              \               │
│       (  A         B  )               │
│        \    ▓▓▓▓▓    /               │
│         └──────────────┘               │
│              Table B                   │
└────────────────────────────────────────┘
        ▓ = Result

EXCEPT (A minus B)
┌────────────────────────────────────────┐
│              Table A                   │
│         ┌──────────────┐               │
│        /▓▓▓▓          \              │
│       (▓▓▓▓▓     B  )               │
│        \▓▓▓▓          /              │
│         └──────────────┘               │
│              Table B                   │
└────────────────────────────────────────┘
```

### UNION

**Definition:** `UNION` combines the result sets of two or more SELECT statements into a single result set. It removes duplicate rows by default. Both queries must have the same number of columns and compatible data types in the corresponding order.

```sql
-- Combine results (removes duplicates)
SELECT customer_id, name FROM us_customers
UNION
SELECT customer_id, name FROM eu_customers;

-- With ORDER BY (at the end)
SELECT customer_id, name FROM us_customers
UNION
SELECT customer_id, name FROM eu_customers
ORDER BY name;
```

### UNION ALL

**Definition:** `UNION ALL` also combines result sets but includes duplicates. It is faster than `UNION` because it doesn't perform the overhead of checking for and removing duplicate rows. Use it when you are sure rows are unique or when you explicitly want duplicates.

```sql
-- Combine results (keeps duplicates)
SELECT product_id FROM orders_2023
UNION ALL
SELECT product_id FROM orders_2024;

-- Use case: combine historical data
SELECT '2023' AS year, * FROM sales_2023
UNION ALL
SELECT '2024' AS year, * FROM sales_2024
ORDER BY year, sale_date;
```

### INTERSECT

**Definition:** `INTERSECT` returns only the rows that appear in the result sets of *both* queries. It effectively finds the common ground between two datasets. Like UNION, columns must match.

```sql
-- Returns only rows present in both queries
-- PostgreSQL, Oracle, SQL Server
SELECT customer_id FROM orders_2023
INTERSECT
SELECT customer_id FROM orders_2024;

-- MySQL workaround
SELECT DISTINCT o1.customer_id
FROM orders_2023 o1
INNER JOIN orders_2024 o2 ON o1.customer_id = o2.customer_id;
```

### EXCEPT / MINUS

**Definition:** `EXCEPT` (or `MINUS` in Oracle) returns rows from the first query that are *not* present in the second query. It performs a set difference operation, useful for finding missing records or discrepancies between tables.

```sql
-- Returns rows from first query not in second
-- PostgreSQL, SQL Server (EXCEPT)
-- Oracle (MINUS)
SELECT customer_id FROM orders_2023
EXCEPT
SELECT customer_id FROM orders_2024;

-- MySQL workaround
SELECT DISTINCT o1.customer_id
FROM orders_2023 o1
LEFT JOIN orders_2024 o2 ON o1.customer_id = o2.customer_id
WHERE o2.customer_id IS NULL;
```

**Best Practices:**
- Columns must have compatible data types
- Number of columns must match
- UNION ALL is faster than UNION (no duplicate removal)
- Use ORDER BY only at the end

---

## 9. Constraints & Keys

### Definition
Constraints enforce rules on data columns to maintain data integrity and accuracy. Keys (Primary, Foreign, Unique) establish relationships between tables and ensure entity uniqueness. Constraints prevent invalid data entry and enforce business rules at the database level rather than application level.

### PRIMARY KEY

**Definition:** A `PRIMARY KEY` is a constraint that uniquely identifies each record in a table. It must contain unique values and cannot contain NULLs. A table can have only one primary key, which may consist of single or multiple columns (composite key).

```sql
-- Single column primary key
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL
);

-- Composite primary key
CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT,
    PRIMARY KEY (order_id, product_id)
);

-- Add primary key to existing table
ALTER TABLE users
ADD PRIMARY KEY (id);

-- Remove primary key
ALTER TABLE users
DROP PRIMARY KEY;
```

### FOREIGN KEY

**Definition:** A `FOREIGN KEY` is a constraint that links two tables together. It identifies a column (or columns) in one table that refers to the PRIMARY KEY in another table. This enforces referential integrity, ensuring that relationships between records remain valid (e.g., an order cannot refer to a non-existent customer).

```sql
-- Basic foreign key
CREATE TABLE orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    total_amount DECIMAL(10,2),
    FOREIGN KEY (user_id) REFERENCES users(id)
);

-- Named foreign key with cascade
CREATE TABLE orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    FOREIGN KEY (user_id) 
        REFERENCES users(id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

-- Foreign key options
ON DELETE CASCADE      -- Delete child rows when parent deleted
ON DELETE SET NULL     -- Set FK to NULL when parent deleted
ON DELETE RESTRICT     -- Prevent parent deletion (default)
ON DELETE NO ACTION    -- Same as RESTRICT
ON UPDATE CASCADE      -- Update FK when parent PK changes

-- Add foreign key to existing table
ALTER TABLE orders
ADD CONSTRAINT fk_user
FOREIGN KEY (user_id) REFERENCES users(id)
    ON DELETE RESTRICT
    ON UPDATE CASCADE;
```

### UNIQUE Constraint

**Definition:** The `UNIQUE` constraint ensures that all values in a column (or a combination of columns) are distinct. Unlike the Primary Key, you can have multiple Unique constraints per table, and depending on the database, they may allow NULL values (often treated as unique).

```sql
-- Column level
CREATE TABLE users (
    id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE,
    username VARCHAR(50) UNIQUE
);

-- Table level (multiple columns)
CREATE TABLE products (
    id INT PRIMARY KEY,
    sku VARCHAR(50),
    warehouse_id INT,
    UNIQUE (sku, warehouse_id)  -- SKU unique per warehouse
);

-- Add unique constraint
ALTER TABLE users
ADD CONSTRAINT uq_email UNIQUE (email);

-- Remove unique constraint
ALTER TABLE users
DROP INDEX uq_email;
```

### NOT NULL & DEFAULT

**Definition:** `NOT NULL` enforces that a column cannot accept NULL values, making it a required field. `DEFAULT` provides a fallback value if no value is specified during an INSERT operation. Together, they ensure data completeness and provide sensible defaults.

```sql
CREATE TABLE products (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,              -- Required
    description TEXT,
    price DECIMAL(10,2) NOT NULL DEFAULT 0,  -- Required with default
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP 
        ON UPDATE CURRENT_TIMESTAMP  -- MySQL only
);

-- Add NOT NULL constraint
ALTER TABLE users
MODIFY email VARCHAR(100) NOT NULL;

-- Add DEFAULT
ALTER TABLE users
ALTER COLUMN is_active SET DEFAULT TRUE;
```

### CHECK Constraint

**Definition:** The `CHECK` constraint limits the value range that can be placed in a column. It validates data against a boolean expression (e.g., `age >= 18`). If the condition evaluates to FALSE, the insert or update operation fails.

```sql
-- Column level check
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT CHECK (age >= 18),
    salary DECIMAL(10,2) CHECK (salary > 0)
);

-- Table level check
CREATE TABLE products (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    price DECIMAL(10,2),
    discount_price DECIMAL(10,2),
    CHECK (discount_price < price),
    CHECK (price >= 0 AND discount_price >= 0)
);

-- Named check constraint
CREATE TABLE users (
    id INT PRIMARY KEY,
    age INT,
    CONSTRAINT chk_age CHECK (age >= 0 AND age <= 150)
);
```

### AUTO_INCREMENT / SERIAL

**Definition:** `AUTO_INCREMENT` (MySQL) or `SERIAL`/`IDENTITY` (PostgreSQL/SQL Server) automatically generates a sequential integer for a column when a new row is inserted. It is the standard way to create surrogate Primary Keys.

```sql
-- MySQL AUTO_INCREMENT
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50)
);

-- PostgreSQL SERIAL
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50)
);

-- SQL Server IDENTITY
CREATE TABLE users (
    id INT PRIMARY KEY IDENTITY(1,1),
    username VARCHAR(50)
);

-- Oracle SEQUENCE (manual)
CREATE SEQUENCE user_seq START WITH 1 INCREMENT BY 1;
CREATE TABLE users (
    id NUMBER PRIMARY KEY,
    username VARCHAR(50)
);
INSERT INTO users (id, username) VALUES (user_seq.NEXTVAL, 'john');
```

**Best Practices:**
- Always use primary keys
- Index foreign key columns
- Use meaningful constraint names
- Choose appropriate ON DELETE behavior
- Use CHECK constraints for data validation
- Avoid NULL in critical fields

---

## 10. Indexes

### Definition
Indexes are data structures that improve query retrieval speed at the cost of additional storage and slower write operations. They work like a book's index, allowing the database to quickly locate rows without scanning entire tables. Indexes are critical for performance on large datasets.

### Index B-Tree Structure

```
B-TREE INDEX STRUCTURE (Simplified)

                    [50]
                   /    \
            [20,35]    [70,85]
            /   |   \   /   |   \
        [10] [25] [40] [60] [75] [90,95]
         |    |    |    |    |     |
       Row1 Row2 Row3 Row4 Row5 Row6,Row7

Properties:
- Balanced tree (all leaf nodes at same depth)
- Sorted data allows binary search
- O(log n) lookup time
- Supports range queries efficiently

INDEX LOOKUP FLOW:
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Query:    │────▶│ Traverse    │────▶│  Leaf Node  │
│ WHERE id=75 │     │ B-Tree      │     │  (Row5)     │
└─────────────┘     └─────────────┘     └─────────────┘
```

### CREATE INDEX

**Definition:** `CREATE INDEX` builds a data structure (typically a B-Tree) that improves the speed of data retrieval operations on a database table at the cost of additional writes and storage space. Use indexes on columns frequently used in WHERE clauses, JOIN conditions, and ORDER BY clauses.

```sql
-- Single column index
CREATE INDEX idx_users_email ON users(email);

-- Unique index
CREATE UNIQUE INDEX idx_users_username ON users(username);

-- Composite index
CREATE INDEX idx_orders_user_date ON orders(user_id, order_date);

-- Partial index (PostgreSQL)
CREATE INDEX idx_active_users ON users(email) WHERE is_active = TRUE;

-- Full-text index (MySQL)
CREATE FULLTEXT INDEX idx_content ON articles(title, content);

-- Prefix index (for long strings)
CREATE INDEX idx_longtext ON logs(message(100));
```

### Index Management

**Definition:** Index management involves viewing, analyzing, and removing indexes. Over-indexing slows down write operations (INSERT, UPDATE, DELETE) because the indexes must be updated transactionally. Regularly reviewing index usage via `EXPLAIN` plans is critical for performance tuning.

```sql
-- View indexes
SHOW INDEX FROM users;  -- MySQL

-- Drop index
DROP INDEX idx_users_email ON users;
ALTER TABLE users DROP INDEX idx_users_email;

-- Rename index (MySQL 5.7+)
ALTER TABLE users RENAME INDEX old_name TO new_name;

-- Analyze table
ANALYZE TABLE users;  -- MySQL

-- Optimize table
OPTIMIZE TABLE users;  -- MySQL
```

### EXPLAIN

**Definition:** The `EXPLAIN` command shows how the database engine executes a query (the query execution plan). It reveals whether indexes are being used (`Index Scan` vs `Seq Scan`), the join order, and the estimated cost. It is the primary tool for debugging slow queries.

```sql
-- Analyze query performance
EXPLAIN SELECT * FROM users WHERE email = 'john@example.com';

-- Detailed analysis (MySQL)
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'john@example.com';

-- Extended explain
EXPLAIN EXTENDED SELECT * FROM users WHERE age > 25;
SHOW WARNINGS;
```

### Query Optimization Flow

```
┌─────────────────────────────────────────────────────────────┐
│                    QUERY OPTIMIZATION FLOW                   │
└─────────────────────────────────────────────────────────────┘

    ┌──────────┐
    │   SQL    │
    │  Query   │
    └────┬─────┘
         │
         ▼
    ┌──────────┐
    │  Parser  │──▶ Syntax validation
    └────┬─────┘
         │
         ▼
    ┌──────────┐
    │   AST    │──▶ Abstract Syntax Tree
    └────┬─────┘
         │
         ▼
    ┌──────────┐
    │ Optimizer│──▶ Choose execution plan
    └────┬─────┘
         │
         ├──▶ Check available indexes
         ├──▶ Estimate row counts
         ├──▶ Calculate costs
         └──▶ Select best plan
         │
         ▼
    ┌──────────┐
    │  Plan    │
    └────┬─────┘
         │
         ▼
    ┌──────────┐
    │ Executor │──▶ Execute plan
    └────┬─────┘
         │
         ▼
    ┌──────────┐
    │  Result  │
    └──────────┘
```

### When to Use Indexes

**Definition:** Indexes should be applied continuously to columns with high cardinality (many unique values) used in filtering and sorting. Avoid indexing columns with low cardinality (e.g., "gender" or "status") or tables with very few rows, where a full table scan might be faster.

**Use indexes for:**
- Primary keys and foreign keys
- Columns frequently used in WHERE, JOIN, ORDER BY
- Columns with high selectivity (many unique values)
- Large tables (> 1000 rows)

**Avoid indexes for:**
- Small tables
- Columns with low selectivity (boolean, status with few values)
- Columns frequently updated (maintenance overhead)
- Columns rarely queried

**Best Practices:**
- Don't over-index (slows down INSERT/UPDATE/DELETE)
- Index columns in order of selectivity
- Use composite indexes for multi-column queries
- Monitor index usage and remove unused indexes
- Consider covering indexes (include all queried columns)

---

## 11. Views, Procedures & Triggers

### Definition
Views are virtual tables based on stored queries that simplify complex queries and provide security by limiting data access. Stored procedures are precompiled SQL routines that encapsulate business logic. Triggers are automated procedures that execute in response to DML events (INSERT, UPDATE, DELETE).

### CREATE VIEW

**Definition:** A `VIEW` is a virtual table based on the result-set of an SQL statement. It contains rows and columns just like a real table but dynamically fetches data when queried. Views simplify complex queries, encapsulate logic, and enhance security by restricting access to specific columns.

```sql
-- Simple view
CREATE VIEW active_users AS
SELECT id, username, email
FROM users
WHERE is_active = TRUE;

-- Complex view with joins
CREATE VIEW customer_orders_summary AS
SELECT 
    c.customer_id,
    c.customer_name,
    COUNT(o.order_id) AS total_orders,
    SUM(o.total_amount) AS total_spent,
    MAX(o.order_date) AS last_order_date
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.customer_name;

-- Use view
SELECT * FROM customer_orders_summary
WHERE total_spent > 1000;

-- Updateable view
CREATE VIEW premium_customers AS
SELECT * FROM customers
WHERE tier = 'premium'
WITH CHECK OPTION;  -- Prevents inserting non-premium customers

-- Drop view
DROP VIEW IF EXISTS active_users;

-- Replace view
CREATE OR REPLACE VIEW active_users AS
SELECT id, username, email, created_at
FROM users
WHERE is_active = TRUE;
```

### Stored Procedures

**Definition:** A Stored Procedure is a prepared SQL code that you can save so the code can be reused over and over again. Unlike views, procedures can verify input parameters, execute procedural logic (IF/ELSE, loops), and modify database state. They reduce network latency by executing logic on the server.

```sql
-- MySQL stored procedure
DELIMITER //
CREATE PROCEDURE GetUserByEmail(IN user_email VARCHAR(100))
BEGIN
    SELECT * FROM users WHERE email = user_email;
END //
DELIMITER ;

-- Call procedure
CALL GetUserByEmail('john@example.com');

-- Procedure with OUT parameter
DELIMITER //
CREATE PROCEDURE GetUserCount(
    IN status BOOLEAN,
    OUT count INT
)
BEGIN
    SELECT COUNT(*) INTO count
    FROM users
    WHERE is_active = status;
END //
DELIMITER ;

-- Call with OUT parameter
CALL GetUserCount(TRUE, @active_count);
SELECT @active_count;

-- Procedure with logic
DELIMITER //
CREATE PROCEDURE PlaceOrder(
    IN p_user_id INT,
    IN p_total DECIMAL(10,2),
    OUT p_order_id INT
)
BEGIN
    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        ROLLBACK;
        RESIGNAL;
    END;
    
    START TRANSACTION;
    
    INSERT INTO orders (user_id, total_amount, order_date)
    VALUES (p_user_id, p_total, CURRENT_DATE);
    
    SET p_order_id = LAST_INSERT_ID();
    
    COMMIT;
END //
DELIMITER ;
```

### Triggers

**Definition:** A Trigger is a special type of stored procedure that automatically runs when an event occurs in the database server. Triggers can be set to run BEFORE or AFTER an INSERT, UPDATE, or DELETE operation. They are often used for auditing changes or enforcing complex integrity constraints.

```sql
-- BEFORE INSERT trigger
CREATE TRIGGER before_user_insert
BEFORE INSERT ON users
FOR EACH ROW
BEGIN
    SET NEW.created_at = CURRENT_TIMESTAMP;
    SET NEW.updated_at = CURRENT_TIMESTAMP;
END;

-- BEFORE UPDATE trigger
CREATE TRIGGER before_user_update
BEFORE UPDATE ON users
FOR EACH ROW
BEGIN
    SET NEW.updated_at = CURRENT_TIMESTAMP;
END;

-- AFTER INSERT trigger (audit log)
CREATE TRIGGER after_order_insert
AFTER INSERT ON orders
FOR EACH ROW
BEGIN
    INSERT INTO order_audit_log (order_id, action, timestamp)
    VALUES (NEW.order_id, 'INSERT', CURRENT_TIMESTAMP);
END;

-- AFTER DELETE trigger
CREATE TRIGGER after_user_delete
AFTER DELETE ON users
FOR EACH ROW
BEGIN
    INSERT INTO deleted_users_archive (user_id, username, deleted_at)
    VALUES (OLD.id, OLD.username, CURRENT_TIMESTAMP);
END;

-- Drop trigger
DROP TRIGGER IF EXISTS before_user_insert;
```

**Best Practices:**
- Use views for complex queries used frequently
- Don't nest views too deeply
- Keep procedures focused and modular
- Document procedure parameters
- Use triggers sparingly (can be hard to debug)
- Consider application-level logic instead of triggers when possible

---

## 12. Transactions

### Definition
Transactions are logical units of work that ensure database integrity by bundling multiple operations into an atomic, consistent, isolated, and durable (ACID) execution. Transactions guarantee that either all operations complete successfully or all changes are rolled back, preventing partial updates that could corrupt data.

### Transaction ACID Properties

```
┌────────────────────────────────────────────────────────────────┐
│                    ACID PROPERTIES                             │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐     │
│  │  ATOMICITY   │    │ CONSISTENCY  │    │  ISOLATION   │     │
│  │              │    │              │    │              │     │
│  │ All or None  │    │ Valid State  │    │ Independent  │     │
│  │              │    │              │    │              │     │
│  │ ┌──┐ ┌──┐   │    │ ┌──┐  ✓ ┌──┐  │    │ T1 ┃ T2 ┃ T3 │     │
│  │ │✓ │ │✓ │   │    │ │✓ │ ──▶ │✓ │  │    │ ━━━╋━━━━╋━━━ │     │
│  │ └──┘ └──┘   │    │ └──┘     └──┘  │    │    ┃    ┃    │     │
│  │              │    │              │    │              │     │
│  │ Either all   │    │ DB remains   │    │ Concurrent   │     │
│  │ operations   │    │ consistent   │    │ transactions │     │
│  │ succeed or   │    │ before and   │    │ don't        │     │
│  │ all fail     │    │ after commit │    │ interfere    │     │
│  └──────────────┘    └──────────────┘    └──────────────┘     │
│                                                                │
│                     ┌──────────────┐                          │
│                     │  DURABILITY  │                          │
│                     │              │                          │
│                     │ Permanent    │                          │
│                     │              │                          │
│                     │ ┌────────┐   │                          │
│                     │ │ COMMIT │──▶│                          │
│                     │ └────────┘   │                          │
│                     │              │                          │
│                     │ Committed    │                          │
│                     │ changes      │                          │
│                     │ survive      │                          │
│                     │ failures     │                          │
│                     └──────────────┘                          │
│                                                                │
└────────────────────────────────────────────────────────────────┘
```

### Basic Transaction Control

**Definition:** Transaction control statements manage the boundaries of a transaction. `START TRANSACTION` (or `BEGIN`) marks the beginning. `COMMIT` saves all changes made since the start. `ROLLBACK` undoes all changes, returning the database to its state before the transaction began.

```sql
-- Start transaction
START TRANSACTION;
-- or
BEGIN;

-- Perform operations
INSERT INTO accounts (user_id, balance) VALUES (1, 1000);
UPDATE accounts SET balance = balance - 100 WHERE user_id = 1;
UPDATE accounts SET balance = balance + 100 WHERE user_id = 2;

-- Commit (save changes)
COMMIT;

-- Or rollback (discard changes)
ROLLBACK;
```

### Savepoints

**Definition:** A `SAVEPOINT` acts as a bookmark within a transaction. You can rollout back to a specific savepoint without rolling back the entire transaction. This is useful for complex workflows where you might want to retry a specific step or handle a partial failure gracefully.

```sql
START TRANSACTION;

INSERT INTO orders (user_id, total) VALUES (1, 100);
SAVEPOINT order_created;

INSERT INTO order_items (order_id, product_id, qty) VALUES (LAST_INSERT_ID(), 1, 2);

-- If item insertion fails, rollback to savepoint
-- ROLLBACK TO SAVEPOINT order_created;

COMMIT;
```

### ACID Properties

| Property | Description |
|----------|-------------|
| **Atomicity** | All operations complete successfully or none do |
| **Consistency** | Database remains in consistent state |
| **Isolation** | Transactions don't interfere with each other |
| **Durability** | Committed changes persist even after system failure |

### Isolation Levels

**Definition:** Isolation levels define how transaction modifications are visible to other concurrent transactions. Standard levels (from lowest to highest isolation) are: Read Uncommitted, Read Committed, Repeatable Read, and Serializable. Higher isolation prevents concurrency anomalies (dirty reads, phantom reads) but reduces performance/throughput.

```sql
-- Set isolation level
SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED;

START TRANSACTION;
-- operations...
COMMIT;

-- Isolation levels:
-- READ UNCOMMITTED - Can see uncommitted changes (dirty reads)
-- READ COMMITTED - Only committed changes visible
-- REPEATABLE READ - Same read gives same result (default in MySQL)
-- SERIALIZABLE - Highest isolation, transactions fully sequential
```

### Error Handling

**Definition:** In stored procedures, you can handle SQL errors using `DECLARE ... HANDLER`. This allows you to define custom logic (like `ROLLBACK`) when an exception occurs (e.g., `SQLEXCEPTION`), ensuring your application can fail gracefully and maintain data integrity.

```sql
DELIMITER //
CREATE PROCEDURE TransferFunds(
    IN from_account INT,
    IN to_account INT,
    IN amount DECIMAL(10,2)
)
BEGIN
    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        ROLLBACK;
        RESIGNAL;
    END;
    
    START TRANSACTION;
    
    UPDATE accounts 
    SET balance = balance - amount 
    WHERE account_id = from_account;
    
    IF ROW_COUNT() = 0 THEN
        ROLLBACK;
        SIGNAL SQLSTATE '45000'
            SET MESSAGE_TEXT = 'Insufficient funds or account not found';
    END IF;
    
    UPDATE accounts 
    SET balance = balance + amount 
    WHERE account_id = to_account;
    
    COMMIT;
END //
DELIMITER ;
```

**Best Practices:**
- Keep transactions as short as possible
- Always commit or rollback
- Handle errors with rollback
- Use appropriate isolation level
- Avoid long-running transactions
- Lock only necessary rows

---

## 13. Database Design

### Definition
Database design is the process of structuring data according to a database model to efficiently store, retrieve, and manage information. Good design minimizes redundancy, ensures data integrity, and supports the application's data access patterns. Key concepts include normalization, relationships, and entity-relationship modeling.

### Entity-Relationship Diagram (ERD)

```
┌─────────────────────────────────────────────────────────────────┐
│              ENTITY-RELATIONSHIP DIAGRAM (ERD)                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌────────────────┐              ┌────────────────┐            │
│  │   CUSTOMER     │              │     ORDER      │            │
│  ├────────────────┤              ├────────────────┤            │
│  │ PK customer_id │──┐           │ PK order_id    │            │
│  │    name        │  │           │ FK customer_id │◄─┐         │
│  │    email       │  │           │    order_date  │  │         │
│  │    phone       │  │           │    total       │  │         │
│  └────────────────┘  │           └────────────────┘  │         │
│          │           │                    │          │         │
│          │           │                    │          │         │
│          │  ┌────────┘                    │          │         │
│          │  │                             │          │         │
│          │  │ 1:M                         │          │         │
│          │  │ (One customer               │          │         │
│          │  │  has many orders)           │          │         │
│          │  │                             │          │         │
│          │  │           ┌─────────────────┘          │         │
│          │  │           │                            │         │
│          │  │           ▼                            │         │
│          │  │    ┌────────────────┐                  │         │
│          │  │    │  ORDER_ITEM    │                  │         │
│          │  │    ├────────────────┤                  │         │
│          │  └───▶│ FK order_id    │                  │         │
│          │       │ FK product_id  │◄─────────────────┘         │
│          │       │    quantity    │                            │
│          │       │    price       │                            │
│          │       └────────────────┘                            │
│          │                                                     │
│          │       M:N Relationship (via junction table)         │
│          └────────────────────────────────────────────────▶    │
│                           ┌────────────────┐                   │
│                           │    PRODUCT     │                   │
│                           ├────────────────┤                   │
│                           │ PK product_id  │                   │
│                           │    name        │                   │
│                           │    price       │                   │
│                           │ FK category_id │──┐                │
│                           └────────────────┘  │                │
│                                               │                │
│                           ┌────────────────┐  │                │
│                           │   CATEGORY     │◄─┘                │
│                           ├────────────────┤                   │
│                           │ PK category_id │                   │
│                           │    name        │                   │
│                           └────────────────┘                   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Table Relationship Types

```
ONE-TO-ONE (1:1)
┌─────────────────────────────────────────────┐
│                                             │
│  ┌─────────────┐        ┌─────────────┐    │
│  │    USER     │────────│ USER_PROFILE│    │
│  ├─────────────┤   1:1  ├─────────────┤    │
│  │ PK user_id  │────────│ PK user_id  │    │
│  │    name     │        │    bio      │    │
│  │    email    │        │    avatar   │    │
│  └─────────────┘        └─────────────┘    │
│                                             │
│  Use Case: Extend entity with optional data │
│                                             │
└─────────────────────────────────────────────┘

ONE-TO-MANY (1:N)
┌─────────────────────────────────────────────┐
│                                             │
│        ┌───────────┐                        │
│        │ CATEGORY  │                        │
│        ├───────────┤                        │
│        │PK cat_id  │◄────────┐              │
│        │   name    │         │              │
│        └───────────┘         │              │
│              │               │              │
│              │ 1:N           │              │
│              │               │              │
│              ▼               │              │
│        ┌───────────┐         │              │
│        │  PRODUCT  │         │              │
│        ├───────────┤         │              │
│        │PK prod_id │         │              │
│        │FK cat_id  │─────────┘              │
│        │   name    │                        │
│        └───────────┘                        │
│                                             │
│  Use Case: Parent-child relationships       │
│                                             │
└─────────────────────────────────────────────┘

MANY-TO-MANY (N:M)
┌─────────────────────────────────────────────┐
│                                             │
│  ┌──────────┐         ┌──────────┐         │
│  │ STUDENT  │         │  COURSE  │         │
│  ├──────────┤         ├──────────┤         │
│  │PK stu_id │◄───────│PK crs_id │         │
│  │   name   │   N:M   │   name   │         │
│  └──────────┘         └──────────┘         │
│       │                     │              │
│       └──────────┬──────────┘              │
│                  ▼                          │
│           ┌──────────┐                     │
│           │ENROLLMENT│                     │
│           ├──────────┤                     │
│           │FK stu_id │                     │
│           │FK crs_id │                     │
│           │  grade   │                     │
│           └──────────┘                     │
│                                             │
│  Use Case: Students enroll in many courses  │
│            Courses have many students       │
│                                             │
└─────────────────────────────────────────────┘
```

### Normalization Levels

```
NORMALIZATION PROGRESSION

┌────────────────────────────────────────────────────────────────┐
│  UNNORMALIZED                                                  │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │ OrderID | Customer | Phone      | Items               │  │
│  │ 1       | John     | 555-1234   | Apple, Banana, Pear │  │
│  └─────────────────────────────────────────────────────────┘  │
│                         │                                      │
│                         ▼                                      │
│  1NF (Atomic Values)                                          │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │ OrderID | Customer | Phone      | Item                │  │
│  │ 1       | John     | 555-1234   | Apple               │  │
│  │ 1       | John     | 555-1234   | Banana              │  │
│  │ 1       | John     | 555-1234   | Pear                │  │
│  └─────────────────────────────────────────────────────────┘  │
│                         │                                      │
│                         ▼                                      │
│  2NF (No Partial Dependencies)                                │
│  ┌──────────────────┐  ┌──────────────────────────────────┐  │
│  │ ORDERS           │  │ ORDER_ITEMS                      │  │
│  ├──────────────────┤  ├──────────────────────────────────┤  │
│  │ OrderID|Customer │  │ OrderID|Item    |Qty             │  │
│  │ 1      |John     │  │ 1      |Apple   |1               │  │
│  │ 1      |John     │  │ 1      |Banana  |2               │  │
│  │ 1      |John     │  │ 1      |Pear    |1               │  │
│  └──────────────────┘  └──────────────────────────────────┘  │
│                         │                                      │
│                         ▼                                      │
│  3NF (No Transitive Dependencies)                             │
│  ┌──────────────────┐  ┌──────────────────┐                 │
│  │ ORDERS           │  │ CUSTOMERS        │                 │
│  ├──────────────────┤  ├──────────────────┤                 │
│  │ OrderID|CustID   │  │ CustID|Name|Phone│                 │
│  │ 1      |101      │  │ 101   |John|555..│                 │
│  └──────────────────┘  └──────────────────┘                 │
│                                                              │
└────────────────────────────────────────────────────────────────┘
```

### Normalization

**Definition:** Normalization is the process of organizing data to reduce redundancy and improve data integrity. It involves dividing large tables into smaller, related tables and defining relationships between them. Common forms are 1NF (atomic values), 2NF (no partial dependencies), and 3NF (no transitive dependencies).

**1NF - First Normal Form:**
- Each cell contains single value (atomic)
- Each column has unique name
- No repeating groups

```sql
-- Not 1NF (multiple phone numbers in one cell)
CREATE TABLE users_bad (
    id INT,
    name VARCHAR(50),
    phone_numbers VARCHAR(200)  -- '123-456, 789-012, 345-678'
);

-- 1NF compliant
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(50)
);

CREATE TABLE user_phones (
    user_id INT,
    phone_number VARCHAR(20),
    PRIMARY KEY (user_id, phone_number)
);
```

**2NF - Second Normal Form:**
- Must be in 1NF
- No partial dependencies (non-key columns depend on entire PK)

```sql
-- Not 2NF (product_name depends only on product_id, not full PK)
CREATE TABLE order_items_bad (
    order_id INT,
    product_id INT,
    product_name VARCHAR(100),  -- Depends only on product_id
    quantity INT,
    PRIMARY KEY (order_id, product_id)
);

-- 2NF compliant
CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT,
    PRIMARY KEY (order_id, product_id)
);

CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100)
);
```

**3NF - Third Normal Form:**
- Must be in 2NF
- No transitive dependencies (non-key columns depend only on PK)

```sql
-- Not 3NF (city depends on zip_code, not directly on user_id)
CREATE TABLE users_bad (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    zip_code VARCHAR(10),
    city VARCHAR(50)  -- Depends on zip_code, not id
);

-- 3NF compliant
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    zip_code VARCHAR(10)
);

CREATE TABLE zip_codes (
    zip_code VARCHAR(10) PRIMARY KEY,
    city VARCHAR(50),
    state VARCHAR(2)
);
```

### Relationships

**Definition:** In a relational database, relationships define how data in one table is connected to data in another. The three main types are **One-to-One** (user has one profile), **One-to-Many** (user has many orders - most common), and **Many-to-Many** (students enroll in courses - requires a pivot/junction table).

**One-to-One:**
```sql
-- Users and user_profiles
CREATE TABLE users (
    id INT PRIMARY KEY,
    username VARCHAR(50),
    email VARCHAR(100)
);

CREATE TABLE user_profiles (
    user_id INT PRIMARY KEY,
    bio TEXT,
    avatar_url VARCHAR(200),
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

**One-to-Many:**
```sql
-- Categories and products
CREATE TABLE categories (
    category_id INT PRIMARY KEY,
    category_name VARCHAR(50)
);

CREATE TABLE products (
    product_id INT PRIMARY KEY,
    category_id INT,
    product_name VARCHAR(100),
    FOREIGN KEY (category_id) REFERENCES categories(category_id)
);
```

**Many-to-Many:**
```sql
-- Students and courses (with junction table)
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100)
);

CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(100)
);

CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    enrollment_date DATE,
    grade VARCHAR(2),
    PRIMARY KEY (student_id, course_id),
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id)
);
```

### ERD (Entity-Relationship Diagram)

Common notation:
- **Rectangles:** Entities (tables)
- **Ellipses:** Attributes (columns)
- **Diamonds:** Relationships
- **Lines:** Connect entities to relationships
- **Crow's foot:** Cardinality (1, many)

Example relationships:
```
User ||--o{ Order : places
Order ||--|{ OrderItem : contains
Product ||--o{ OrderItem : included_in
Category ||--o{ Product : categorizes
```

**Best Practices:**
- Design for 3NF, denormalize only when necessary
- Use appropriate data types
- Name tables and columns consistently
- Document relationships
- Plan for growth
- Consider query patterns when designing

---

## 14. Advanced Topics

### Definition
Advanced SQL topics extend beyond basic CRUD operations to include analytical capabilities, hierarchical data handling, and complex data transformations. Window functions perform calculations across row sets, CTEs improve query readability, and recursive queries handle tree-structured data.

### SQL Execution Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                    SQL QUERY EXECUTION FLOW                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   1. FROM & JOINs                                               │
│      └─▶ Identify source tables and perform joins              │
│      └─▶ Create virtual table combining all rows               │
│                                                                 │
│   2. WHERE                                                      │
│      └─▶ Filter rows based on conditions                       │
│      └─▶ Remove rows that don't match                          │
│                                                                 │
│   3. GROUP BY                                                   │
│      └─▶ Group remaining rows by specified columns             │
│      └─▶ Create summary rows for each group                    │
│                                                                 │
│   4. HAVING                                                     │
│      └─▶ Filter groups based on aggregate conditions           │
│      └─▶ Remove groups that don't meet criteria                │
│                                                                 │
│   5. SELECT                                                     │
│      └─▶ Calculate expressions and aliases                     │
│      └─▶ Apply DISTINCT if specified                           │
│                                                                 │
│   6. ORDER BY                                                   │
│      └─▶ Sort result set by specified columns                  │
│      └─▶ Apply ASC/DESC ordering                               │
│                                                                 │
│   7. LIMIT / OFFSET                                             │
│      └─▶ Restrict number of rows returned                      │
│      └─▶ Skip specified number of rows                         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Window Functions

**Definition:** Window functions perform calculations across a set of table rows that are related to the current row. Unlike aggregate functions, window functions do not cause rows to become grouped into a single output row — the rows retain their separate identities. Common examples include `ROW_NUMBER()`, `RANK()`, and running totals.

```sql
-- ROW_NUMBER() - unique sequential number
SELECT 
    product_name,
    price,
    category,
    ROW_NUMBER() OVER (ORDER BY price DESC) AS price_rank
FROM products;

-- ROW_NUMBER() with PARTITION
SELECT 
    product_name,
    price,
    category,
    ROW_NUMBER() OVER (PARTITION BY category ORDER BY price DESC) 
        AS category_rank
FROM products;

-- RANK() and DENSE_RANK()
SELECT 
    product_name,
    price,
    RANK() OVER (ORDER BY price DESC) AS rank_with_gaps,
    DENSE_RANK() OVER (ORDER BY price DESC) AS rank_no_gaps
FROM products;

-- LAG() and LEAD() - access previous/next rows
SELECT 
    order_date,
    total_amount,
    LAG(total_amount, 1) OVER (ORDER BY order_date) AS prev_amount,
    total_amount - LAG(total_amount, 1) OVER (ORDER BY order_date) 
        AS change
FROM orders;

-- Running totals
SELECT 
    order_date,
    total_amount,
    SUM(total_amount) OVER (ORDER BY order_date) AS running_total
FROM orders;

-- Moving averages
SELECT 
    order_date,
    total_amount,
    AVG(total_amount) OVER (
        ORDER BY order_date 
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) AS 7_day_avg
FROM daily_sales;

-- FIRST_VALUE and LAST_VALUE
SELECT 
    category,
    product_name,
    price,
    FIRST_VALUE(product_name) OVER (
        PARTITION BY category 
        ORDER BY price DESC
    ) AS most_expensive_in_category
FROM products;

-- NTILE - percentile buckets
SELECT 
    product_name,
    price,
    NTILE(4) OVER (ORDER BY price) AS price_quartile
FROM products;
```

### CTEs (Common Table Expressions)

```sql
-- Basic CTE
WITH active_users AS (
    SELECT * FROM users WHERE is_active = TRUE
)
SELECT * FROM active_users WHERE age > 25;

-- Multiple CTEs
WITH 
user_orders AS (
    SELECT user_id, COUNT(*) AS order_count
    FROM orders
    GROUP BY user_id
),
user_spending AS (
    SELECT user_id, SUM(total_amount) AS total_spent
    FROM orders
    GROUP BY user_id
)
SELECT 
    u.username,
    COALESCE(uo.order_count, 0) AS orders,
    COALESCE(us.total_spent, 0) AS spent
FROM users u
LEFT JOIN user_orders uo ON u.id = uo.user_id
LEFT JOIN user_spending us ON u.id = us.user_id;

-- Recursive CTE
WITH RECURSIVE employee_hierarchy AS (
    -- Anchor member: top-level employees
    SELECT 
        employee_id,
        name,
        manager_id,
        0 AS level,
        CAST(name AS CHAR(200)) AS hierarchy_path
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive member: employees with managers
    SELECT 
        e.employee_id,
        e.name,
        e.manager_id,
        eh.level + 1,
        CONCAT(eh.hierarchy_path, ' > ', e.name)
    FROM employees e
    INNER JOIN employee_hierarchy eh ON e.manager_id = eh.employee_id
)
SELECT * FROM employee_hierarchy
ORDER BY hierarchy_path;

-- CTE with window functions
WITH ranked_products AS (
    SELECT 
        category,
        product_name,
        price,
        RANK() OVER (PARTITION BY category ORDER BY price DESC) AS rank
    FROM products
)
SELECT * FROM ranked_products WHERE rank <= 3;
```

**Best Practices:**
- Use window functions instead of self-joins when possible
- CTEs improve readability for complex queries
- Recursive CTEs are powerful for hierarchical data
- Window functions don't change row count (unlike GROUP BY)
- Use EXPLAIN to verify performance of window functions

---

## 🔑 Key Takeaways

1. **SQL is declarative** - specify what you want, not how to get it
2. **Indexes are crucial** for performance on large tables
3. **Normalization** reduces redundancy, but denormalize for read performance when needed
4. **Transactions** ensure data integrity - use them for multi-step operations
5. **JOINs** are more efficient than subqueries in most cases
6. **Window functions** enable advanced analytics without self-joins
7. **Always use WHERE** with UPDATE and DELETE statements
8. **Plan for growth** - design schemas that can scale

---

**Resources:**
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [SQLite Documentation](https://www.sqlite.org/docs.html)
- [SQL Zoo](https://sqlzoo.net/) - Interactive tutorials
- [DB Fiddle](https://www.db-fiddle.com/) - Online SQL playground
