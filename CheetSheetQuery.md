Here’s a reorganized and structured README with the provided queries, explained in a clear, readable, and well-formatted way:

---

# PostgreSQL SQL Queries Cheat Sheet

## Table of Contents

- [Retrieving Data](#retrieving-data)
  - [Selecting Columns](#selecting-columns)
  - [Ordering Results](#ordering-results)
  - [Removing Duplicates](#removing-duplicates)
  - [Filtering Results with WHERE](#filtering-results-with-where)
  - [Using Comparisons](#using-comparisons)
  - [LIMIT and OFFSET](#limit-and-offset)
- [Working with Multiple Values](#working-with-multiple-values)
  - [IN Clause](#in-clause)
  - [BETWEEN Clause](#between-clause)
  - [LIKE and ILIKE](#like-and-ilike)
- [Grouping and Aggregating Data](#grouping-and-aggregating-data)
  - [GROUP BY](#group-by)
  - [HAVING Clause](#having-clause)
  - [Aggregation Functions](#aggregation-functions)
- [Handling NULL Values](#handling-null-values)
  - [COALESCE](#coalesce)
  - [NULLIF](#nullif)
- [Date and Time Functions](#date-and-time-functions)
  - [NOW()](#now)
  - [EXTRACT](#extract)
  - [AGE](#age)
  - [INTERVAL](#interval)
- [Modifying Data](#modifying-data)
  - [DELETE](#delete)
  - [UPDATE](#update)
  - [ON CONFLICT](#on-conflict)
- [Working with Keys](#working-with-keys)
  - [Primary Key](#primary-key)
  - [Foreign Key](#foreign-key)
- [Joining Tables](#joining-tables)
  - [INNER JOIN](#inner-join)
  - [LEFT JOIN](#left-join)
- [Advanced](#advanced)
  - [Exporting Data to CSV](#exporting-data-to-csv)
  - [Sequence Operations](#sequence-operations)

---

## Retrieving Data

### Selecting Columns

- Retrieve all data from a table:
  ```sql
  SELECT * FROM person;
  ```

- Retrieve specific columns:
  ```sql
  SELECT first_name FROM person;
  ```

### Ordering Results

- Order results by a specific column in descending order (default is ascending):
  ```sql
  SELECT * FROM person ORDER BY id DESC;
  ```

- Order by multiple columns:
  ```sql
  SELECT * FROM person ORDER BY first_name, email DESC;
  ```

### Removing Duplicates

- Remove duplicates from a query:
  ```sql
  SELECT DISTINCT country_of_birth FROM person;
  ```

- Combine `DISTINCT` with `ORDER BY`:
  ```sql
  SELECT DISTINCT country_of_birth FROM person ORDER BY country_of_birth;
  ```

### Filtering Results with WHERE

- Filter data based on a condition:
  ```sql
  SELECT * FROM person WHERE gender = 'Male';
  ```

- Filter with multiple conditions using AND:
  ```sql
  SELECT * FROM person WHERE gender = 'Male' AND country_of_birth = 'Jordan';
  ```

- Combine conditions with parentheses:
  ```sql
  SELECT * FROM person WHERE gender = 'Male' AND (country_of_birth = 'Jordan' OR country_of_birth = 'Japan');
  ```

### Using Comparisons

- Common comparison operators:
  - `=` (equal)
  - `<>` (not equal)
  - `>` (greater than)
  - `<` (less than)

---

## LIMIT and OFFSET

- Limit the number of rows returned:
  ```sql
  SELECT * FROM person LIMIT 10;
  ```

- Skip a number of rows and then limit:
  ```sql
  SELECT * FROM person LIMIT 5 OFFSET 5;
  ```

---

## Working with Multiple Values

### IN Clause

- Select rows where a column matches any value in a list:
  ```sql
  SELECT * FROM person WHERE country_of_birth IN ('China', 'Thailand');
  ```

### BETWEEN Clause

- Select rows where a column value is between a range:
  ```sql
  SELECT * FROM person WHERE date_of_birth BETWEEN '2000-01-01' AND '2024-01-01';
  ```

### LIKE and ILIKE

- Use `LIKE` to match patterns with `%` (wildcard):
  ```sql
  SELECT * FROM person WHERE email LIKE '%.com';
  ```

- Specify character length with `_`:
  ```sql
  SELECT * FROM person WHERE email LIKE '____.%';
  ```

- Use `ILIKE` for case-insensitive pattern matching:
  ```sql
  SELECT * FROM person WHERE email ILIKE '%.COM';
  ```

---

## Grouping and Aggregating Data

### GROUP BY

- Group data by a specific column and count occurrences:
  ```sql
  SELECT country_of_birth, COUNT(*) FROM person GROUP BY country_of_birth ORDER BY country_of_birth;
  ```

### HAVING Clause

- Add an additional filter to grouped data:
  ```sql
  SELECT country_of_birth, COUNT(*) FROM person GROUP BY country_of_birth HAVING COUNT(*) > 4 ORDER BY country_of_birth;
  ```

### Aggregation Functions

- Common aggregation functions:
  - `MIN()`: Minimum value
  - `MAX()`: Maximum value
  - `AVG()`: Average value
  - `COUNT()`: Count rows
  - `SUM()`: Sum values

- Example:
  ```sql
  SELECT make, MAX(price) FROM car GROUP BY make;
  ```

---

## Handling NULL Values

### COALESCE

- Replace NULL values with a default value:
  ```sql
  SELECT COALESCE(email, 'NOT FOUND') FROM person;
  ```

### NULLIF

- Compare two values and return `NULL` if they are equal:
  ```sql
  SELECT NULLIF(10, 10); -- Returns NULL
  SELECT NULLIF(10, 20); -- Returns 10
  ```

---

## Date and Time Functions

### NOW()

- Get the current timestamp:
  ```sql
  SELECT NOW();
  ```

- Extract only the date or time:
  ```sql
  SELECT NOW()::DATE;
  SELECT NOW()::TIME;
  ```

### EXTRACT

- Extract parts of a timestamp (e.g., month, year):
  ```sql
  SELECT EXTRACT(MONTH FROM NOW());
  ```

### AGE

- Calculate the age based on the current date:
  ```sql
  SELECT first_name, AGE(NOW(), date_of_birth) AS age FROM person;
  ```

- Extract the year difference:
  ```sql
  SELECT first_name, EXTRACT(YEAR FROM AGE(NOW(), date_of_birth)) AS age FROM person;
  ```

### INTERVAL

- Add or subtract time intervals:
  ```sql
  SELECT NOW() - INTERVAL '1 YEAR';
  ```

---

## Modifying Data

### DELETE

- Delete records from a table:
  ```sql
  DELETE FROM person WHERE id = 1;
  ```

### UPDATE

- Update records in a table:
  ```sql
  UPDATE person SET email = 'newemail@example.com' WHERE id = 2;
  ```

### ON CONFLICT

- Handle conflicts when inserting data:
  ```sql
  INSERT INTO person (id, first_name, email) VALUES (3, 'Fannie', NULL)
  ON CONFLICT DO NOTHING;
  ```

- Use conflict handling to update records:
  ```sql
  INSERT INTO person (id, first_name) VALUES (3, 'Asaad')
  ON CONFLICT (id) DO UPDATE SET first_name = EXCLUDED.first_name;
  ```

---

## Working with Keys

### Primary Key

- Add a primary key to a table:
  ```sql
  ALTER TABLE person ADD PRIMARY KEY (id);
  ```

### Foreign Key

- Add a foreign key to a table:
  ```sql
  ALTER TABLE person ADD CONSTRAINT fk_car FOREIGN KEY (car_id) REFERENCES car(id);
  ```

---

## Joining Tables

### INNER JOIN

- Combine rows from two tables where a foreign key matches:
  ```sql
  SELECT * FROM person JOIN car ON person.car_id = car.id;
  ```

### LEFT JOIN

- Return all rows from the left table and matching rows from the right table:
  ```sql
  SELECT * FROM person LEFT JOIN car ON person.car_id = car.id;
  ```

---

## Advanced

### Exporting Data to CSV

- Export query results to a CSV file:
  ```sql
  \copy (SELECT * FROM person LEFT JOIN car ON person.car_id = car.id) TO '/home/user/database/result.csv' DELIMITER ',' CSV HEADER;
  ```

### Sequence Operations

- Check the next sequence value:
  ```sql
  SELECT nextval('person_id_seq'::regclass);
  ```

- Reset sequence to a specific value:
  ```sql
  ALTER SEQUENCE person_id_seq RESTART WITH 3;
  ```

---

This structure should make your queries much easier to understand and navigate!
