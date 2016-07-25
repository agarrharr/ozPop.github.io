---
layout: post
title: SQL Basics
---

From SQL Getting Started section on Learn

## Creating database and tables basics

----

### Column name conventions

* Always use lowercase letters when referring to columns in a database
* Link multiple words together using underscores rather than spaces

### Creating a database + table

Create database by typing

`$ sqlite3 database_name.db`

To create a table we need to specify some column names
*(the use of capitalization is arbitrary, but it is a convention to help separate the SQL commands from the names we make up for our tables and columns)*

```Sql
CREATE TABLE cats (
    id INTEGER PRIMARY KEY,
            name    TEXT,
            age     INTEGER
    );
```

###### NOTE: sql commands when typed in terminal have to be preceded by a `.` 

`.schema`, `.tables`, `.quit` or `.help`

<br>

### Altering a table

`ALTER TABLE table_name ADD COLUMN column_name DATA-TYPE`


```Sql
ALTER TABLE cats ADD COLUMN breed TEXT
```

###### NOTE: Sql ALTER statement updates the CREATE statement. altering or deleting a column
is tricky in sqlite3. For now, the recommended approach is to re-create the whole table.

[For more on ALTER](https://www.sqlite.org/lang_altertable.html)

<p></p>

### Deleting a table

```Sql
DROP TABLE table_name;
```

### Creating a table from a file

Once you have created a file some_file_name.sql using your favorite text editor.
You can execute that file and create a table by running the command:

`$ sqlite3 database_name.db < some_file_name.sql`

<br>

## SQL Data Types

----

The practice of explicitly declaring a type is known as "typing." This gives us
some control over our data. Typing not only informs our database of the kind of
data we plan to store in a column but it also restricts it.

Datatypes basic categories:

* TEXT - plain text
* INTEGER - whole numbers
* REAL - decimal numbers up to 15 characters long
* BLOB - for holding binary data

[For more on Datatypes](http://www.sqlite.org/datatype3.html)

<br>

## SQL Inserting, Updating and Selecting

### Inserting

To insert into existing table use the following:

```sql
INSERT INTO table_name (name, age) VALUES ('Thor', 90);
```

```sql
INSERT INTO cats (name, age, breed) VALUES ('Maru', 3, 'Scottish Fold');
```

###### NOTE: Primary Key columns are auto-incrementing

### Selecting using `SELECT` statement


`SELECT [names_of_columns] FROM [table_name]`

```sql
SELECT id, name, age FROM cats;
```

To select all columns use:

```sql
SELECT * FROM cats;
```
To select just certain columns:

```sql
SELECT name FROM cats;
```

###### NOTE: Use DISTINCT statement to select unique values only.

```sql
SELECT DISTICT name FROM cats;
```

<p></p>

### Selecting based on conditions with `WHERE` clause

`SELECT * FROM [table name] WHERE [column name] = [some value];`


```sql
SELECT * FROM cats WHERE name = "Maru";
```

###### NOTE: Comparison operators like `<` or `>` select specific data.

```sql
SELECT * FROM cats WHERE age < 2;
```

<p></p>

### Updating data using `UPDATE` keyword

`UPDATE [table name] SET [column name] = [new value] WHERE [column name] = [value];`

```sql
UPDATE cats SET name = "Hana" WHERE name = "Hannah";
```

### Deleting data using `DELETE` keyword

`DELETE FROM [table name] WHERE [column name] = [value];`

```sql
DELETE FROM cats WHERE id = 3;
```

<br>

## Basic SQL Queries

----

###### NOTE: To *format output* of your `SELECT` statements use the blow options

### Changing cli output (display)

```
.header on       # output the name of each column
.mode column     # now we are in column mode, enabling us to run the next two .width commands
.width auto      # adjusts and normalizes column width
# or
.width NUM1, NUM2 # customize column width
```
<p></p>

### ORDER BY

`SELECT column_name FROM table_name ORDER BY column_name ASC|DESC;`


```sql
SELECT * FROM cats ORDER BY age;
```

`ASC` or `DESC` keywords change order. ORDER BY defaults to ascending

```sql
SELECT * FROM cats ORDER BY age DESC;
```
<p></p>

### LIMIT

`LIMIT` is used to determine the number of records you want to return from a dataset.

```sql
SELECT * FROM cats ORDER BY age DESC LIMIT 1;
```
<p></p>

### BETWEEN

`SELECT column_name(s) FROM table_name WHERE column_name BETWEEN value1 AND value2;`

```sql
SELECT name FROM cats WHERE age BETWEEN 1 AND 3;
```
<p></p>

### NULL

```sql
INSERT INTO cats (name, age, breed) VALUES (NULL, NULL, "Tabby");
```

We can select using NULL too

```sql
SELECT * FROM cats WHERE name IS NULL;
```
<br>

## Aggregate functions COUNT and GROUP BY

Aggregate functions perform a calculation on specified values, queried from a database table.

### COUNT

Count is a SQL aggregate function. `COUNT` will count the number of records that 
meet certain condition.


`SELECT COUNT([column name]) FROM [table name] WHERE [column name] = [value]`

```sql
SELECT COUNT(owner_id) FROM cats WHERE owner_id = 1;
```

```sql
SELECT COUNT(name) FROM cats;
```

```sql
SELECT COUNT(*) FROM cats WHERE net_worth > 1000000;
```
<p></p>

### AVG

`AVG` returns the average value of a column.

`SELECT AVG(column_name) FROM table_name;`

```sql
SELECT AVG(net_worth) FROM cats;
```
###### NOTE: using `AS` keyword we can rename the column

```sql
SELECT AVG(net_worth) AS average_net_worth FROM cats;
```
<p></p>

### SUM

`SUM` returns the sum of a column.

`SELECT SUM(column_name) FROM table_name;`

```sql
SELECT SUM(net_worth) FROM cats;
```
<p></p>

### MIN and MAX

`MIN` and `MAX` return minimum and maximum from specified column

`SELECT MIN(column_name) FROM table_name;`

`SELECT MAX(column_name) FROM table_name;`

```sql
SELECT MIN(net_worth) FROM cats;
```
<p></p>

### GROUP BY

```sql
SELECT breed, COUNT(breed) FROM cats GROUP BY breed;
```

```sql
SELECT breed, owner_id, COUNT(breed) FROM cats GROUP BY breed, owner_id;
```
<p></p>

### NOTE ON `SELECT`

```sql
SELECT cats.name FROM cats;
```

###### NOTE: SQLite allows us to select tableName.columnName

 Combine results from two different tables into one output

```sql
SELECT cats.name, dogs.name FROM cats, dogs;
```




SOURCE: learn.co Full Stack Web Development, SQL getting started section

