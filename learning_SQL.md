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

Basic Math Operators,

`+`, `-`, `*`, `/`, `^` Exponent, `|/` Square root,`@` Absolute value, `%` Remainder.
