# Learning SQL and PostegreSQL

## Introduction

Here we have `client` which send `SQL Queries` to the `Server (Database)`, and the data is returned from there.

`SQL` is the language used to interact with the databases.

Before designing a database,

- What kind of thing we are storing ?
- What properties does these things have ?
- What type of data each of these properties contain ?

`Table` is a collection of records, each `Table` has multiple `Columns` which holds one property, each value in a `Column` has a specific data type.

### Creating Table

```sql
CREATE TABLE cities(
  name VARCHAR(20),
  country VARCHAR(20),
  population INTEGER,
  area INTEGER
);
```

Here `CREATE TABLE` is key words and `cities` is a identifier, `VARCHAR` variable length character.

### Inserting Data Into Table

```sql
INSERT INTO cities(name, country, population, area ) VALUES ('Tokyo', 'Japan', 38505000, 8223);
```

### Retrieving Data From Table

```sql
SELECT * FROM cities;

SELECT name, country FROM cities;
```

### Calculated Columns

```sql
SELECT value1 / value2 AS division_result FROM scores;
```

Basic and Comparison Math Operators,

`+`, `-`, `*`, `/`, `^` Exponent, `|/` Square root,`@` Absolute value, `%` Remainder, `<>` and `!=` Not equal to, `IN` the value present in a list, `NOT IN` the value not present in a list, `BETWEEN` the value between two other values, `>`, `<`, `>=`, `<=`, `=` Equal to.

### Filtering Results

```sql
SELECT * FROM cities
WHERE area > 2000;
```

Here `FROM` is executed first, then the `WHERE` and lastly `SELECT`,Combining multiple `WHERE` statement with `AND`, `OR`, calculations can also be done in `WHERE` statements.

```sql
SELECT *
FROM cities
WHERE name NOT IN ('a', 'b')
AND name = 'c';
```

### Updating rows

```sql
UPDATE cities
SET area = 2332
WHERE area = 5343;
```

### Deleting rows

```sql
DELETE FROM cities
WHERE name = 'a';
```

### Deleting a table

```sql
DROP TABLE cities;
```

## Database Project

### Types of relationships

`One-to-many relationship`, `Many-to-one-relationship`, these both are opposite to each other, `One-to-one relationship`, `Many-to-many relationship`.

### Primary Keys and Foreign Keys

`Primary key`, uniquely identifies a row in table, `Foreign Key` identifies other record in another table that this table is associated with.

`Primary Keys`,

- Each row in every table has one primary key
- No other row in the same table can have same value
- Commonly it's called as `id`
- Either an integer or uuid
- It will never change

`Foreign Keys`,

- Rows only have this key if they belong to another record
- Many rows can have same foreign keys
- Exactly equal to the referenced primary key
- It will change if the relationship changes

Here `SERIAL` uniquely creates a value for each row,

Creating a table with `PRIMARY KEY`,

```sql
CREATE TABLE users(
  id SERIAL PRIMARY KEY,
  username VARCHAR(50)
)

INSERT INTO users(username)
VALUES ('a'), ('b'), ('c');
```

Creating a table with `FOREIGN KEY`,

```sql
CREATE TABLE photos(
  id SERIAL PRIMARY KEY,
  url VARCHAR(200),
  userId INTEGER REFERENCES users(id)
);

INSERT INTO photos(url, userId)
VALUES ('aa.io', 2), ('bb.o', 1);
```

Retrieving values from tables,

```sql
SELECT *
FROM photos
WHERE userID = 1;
```

```sql
SELECT *
FROM photos
JOIN users ON users.id = photos.user_id;
```

### Constraints around deletion

- `ON DELETE RESTRICT`, Throw an error
- `ON DELETE NO ACTION`, Throw an error
- `ON DELETE CASCADE`, Delete the associated data
- `ON DELETE SET NULL`, set the value to `NULL`
- `ON DELETE SET DEFAULT`, set the value to `default value`

Setting delete constraints, it should be set on `FOREIGN KEY`,

```sql
CREATE TABLE cities(
  country_id INTEGER REFERENCES country(id) ON DELETE CASCADE
);
```

## JOINS

```sql
SELECT *
FROM comments
JOIN users ON users.id = comments.user_id;
```

### Different kinds of JOINS

`Inner Join`,

```sql
SELECT *
FROM comments
INNER JOIN users ON users.id = comments.user_id;
```

Here the row that doesn't match up with the query is dropped.

`Left Outer Join`,

```sql
SELECT url, username
FROM photos
LEFT JOIN users ON users.id = photos.user_id;
```

If some row doesn't match up with the query, then it is associated with `NULL` value.

The order of table in `FROM`, and `JOIN` matters.

`Right Outer Join`,

```sql
SELECT url, username
FROM photos
RIGHT JOIN users ON users.id = photos.user_id;
```

It is the opposite of `Left Outer Join`.

The order of table in `FROM`, and `JOIN` matters.

`Full Outer Join`,

```sql
SELECT url, username
FROM photos
FULL JOIN users ON users.id = photos.user_id;
```

It combines all the rows.

## Grouping and Aggregation

`GROUP BY` finds all the unique id's and then creates a separate group for them.

```sql
SELECT user_id
FROM comments
GROUP BY user_id;
```

`Aggregation` Functions,

- `COUNT()`, doesn't work on `NULL`
- `SUM()`
- `AVG()`
- `MIN()`
- `MAX()`

Combining both `Aggregate` functions and `GROUP BY`,

```sql
SELECT COUNT(*)
FROM comments
GROUP BY user_id;
```

The `HAVING` clause is similar to `WHERE` but used with the `GROUP BY` clause.

## Sorting

`ORDER BY` sorts the table, `ASC` and `DESC`.

```sql
SELECT *
FROM products
ORDER BY price DESC;
```

`OFFSET` to skip some numbers, `LIMIT` to limit the number of records in result.

```sql
SELECT *
FROM products
OFFSET 40;
```

Here it skips first 40 records,

```sql
SELECT *
FROM products
LIMIT 10;
```

Only first 10 records,

## UNIONS and INTERSECTIONS

`UNION` combines two results,

```sql
(
  SELECT *
  FROM products
  ORDER BY price DESC
  LIMIT 4
)
UNION ALL
(
  SELECT *
  FROM products
  ORDER BY price / weight DESC
  LIMIT 4
);
```

other keywords,

- `UNION`, join all rows, remove duplicates
- `UNION ALL`
- `INTERSECT`, Find common rows and join them, remove duplicates
- `INTERSECT ALL`
- `EXCEPT`, find the rows that are in first query, but not in second query, remove duplicates
- `EXCEPT ALL`

## Sub queries

```sql
SELECT price
FROM department
WHERE price > (
  SELECT MAX(price)
  FROM department
  WHERE department_s = 'Cloths'
);
```

The `SELECT` should contain a sub query that has a single value, `FROM` should contain a sub query that produces many rows, many columns, or many rows, single column, but in `FROM` the sub query needs to be aliased, and it should be compatible with the `SELECT` and `WHERE`.

The sub query can also access data from outside query.

## Distinct, Greatest, Least, Case Keywords

```sql
SELECT DISTINCT cities
FROM countries;
```

```sql
SELECT GREATEST(10, 20, 30);
```

```sql
SELECT LEAST(10, 20, 30);
```

```sql
SELECT price,
  CASE
    WHEN price > 600 THEN 'High'
    WHEN price < 300 THEN 'Low'
    ELSE 'Very Low'
    END
FROM store;
```

## Postgres

### Data types

`Numbers`, `Currency`, `Binary`, `Date/Time`, `Character`, `JSON`, `Geometric`, `Range`, `Arrays`, `Boolean`, `XML`, `UUID`, `CHAR` etc.

`Rules`,

- `SERIAL`, for id's
- `INTEGER`, to store a number without decimal
- `NUMERIC` or `DOUBLE`, to store a number with decimal
- `CHAR(5)`
- `VARCHAR`
- `TEXT`
- `true, yes, on, 1, t, y`
- `false, no, off, 0, f, n`
- `NULL`

Storing Dates,

The `date` formats are, `1980-11-20`, `NOV-20-1980`, `20-NOV-1980`, `1980-November-20`, `November 20, 1980` etcetera.

The `time` formats are, `01:23 AM`, `20:34`, `20:34 UTC`.
