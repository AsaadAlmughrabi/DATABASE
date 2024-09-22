# Database Notes

## Table of Contents
- [Creating and Deleting a Database](#creating-and-deleting-a-database)
- [PostgreSQL Overview](#postgresql-overview)
- [Primary Key](#primary-key)
- [SQL Overview](#sql-overview)
- [Relational Databases](#relational-databases)
- [Common PostgreSQL Commands](#common-postgresql-commands)
- [How Data is Stored](#how-data-is-stored)
- [SQL Joins](#sql-joins)
  - [INNER JOIN](#inner-join)
  - [LEFT JOIN](#left-join)
- [Constraints](#constraints)
  - [Unique Constraint](#unique-constraint)
  - [Check Constraint](#check-constraint)
  - [Foreign Key](#foreign-key)

---

## Creating and Deleting a Database

- **Create a Database**:  
  ```sql
  CREATE DATABASE database_name;
  ```

- **Delete a Database**:  
  ```sql
  DROP DATABASE database_name;
  ```

---

## PostgreSQL Overview

- **PostgreSQL**:  
  PostgreSQL is an object-relational database management system (ORDBMS). It is modern, open-source, and widely used for handling relational data efficiently.  
  - **Type**: Object-relational DBMS
  - **Features**: Modern, Open-source

---

## Primary Key

- **Definition**:  
  A primary key is a constraint in SQL that uniquely identifies each record in a table.

- **Rules**:
  1. **Uniqueness**: Every value in the primary key column must be unique across all records in the table.
  2. **Not Null**: The primary key cannot contain NULL values. Each record must have a valid, non-null primary key.

- **Characteristics**:
  - A table can only have one primary key.
  - The primary key can consist of one column (simple primary key) or multiple columns (composite primary key).
  - It is used to establish relationships between tables (using foreign keys).

---

## SQL Overview

- **SQL (Structured Query Language)**:  
  SQL is used to store, manipulate, and retrieve data in a relational database. It is the standard language for managing data in relational databases. 

- **Purpose**:
  - Storing and managing data
  - Retrieving and manipulating data
  - Querying relational databases

---

## Relational Databases

- **Definition**:  
  A relational database is a system where data is stored in related tables, and relationships can be established between one or more tables.

---

## Common PostgreSQL Commands

- **List Databases**:  
  `\l` - Lists all databases.

- **Connect to a Database**:  
  `\c database_name` - Connects to a specific database.

- **List Records Inside a Table**:  
  `\d table_name` - Describes the structure of a table.

- **Expand Query Results**:  
  `\x` - Expands the display of query results.

---

## How Data is Stored

- **Data is stored in tables**, which consist of:
  - **Columns**: Attributes that describe the data.
  - **Rows**: The actual data entries within the table.

- **Data Storage**:  
  Data is usually stored on a server, and we can retrieve, manipulate, and delete data from the server using queries.

---

## SQL Joins

### INNER JOIN
- **Definition**:  
  An INNER JOIN is used to combine rows from two or more tables based on a related column. It only returns rows where there are matching values in both tables.

- **How It Works**:
  1. **Tables**: At least two tables are involved (e.g., Customers and Orders).
  2. **Join Condition**: A condition (usually matching a primary key from one table to a foreign key in the other) relates the tables.

- **Example**:
  ```sql
  SELECT columns
  FROM table1
  INNER JOIN table2
  ON table1.common_column = table2.common_column;
  ```

### LEFT JOIN (LEFT OUTER JOIN)
- **Definition**:  
  A LEFT JOIN returns all rows from the left table and matched rows from the right table. If there is no match, columns from the right table will contain `NULL`.

- **How It Works**:
  1. **Tables**: At least two tables are involved (e.g., Customers and Orders).
  2. **Join Condition**: Specifies how the tables relate, similar to INNER JOIN.

- **Result**:  
  All rows from the left table will appear in the result, and unmatched rows from the right table will show `NULL` values.

- **Example**:
  ```sql
  SELECT columns
  FROM table1
  LEFT JOIN table2
  ON table1.common_column = table2.common_column;
  ```

---

## Constraints

### Unique Constraint
- **Definition**:  
  A UNIQUE constraint ensures that all values in a column are unique across the table, preventing duplicate entries in the specified column.

---

### Check Constraint
- **Definition**:  
  A CHECK constraint enforces a rule on values in a column, ensuring that all values meet a specific condition before being inserted or updated.

---

### Foreign Key
- **Definition**:  
  A foreign key is a column (or a set of columns) in a table that references a primary key in another table, establishing a relationship between the two tables.

